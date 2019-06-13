Un'ALV è un metodo di output per mostrare tabelle o dati a schermo, dopo un'elaborazione. Esistino varie classi (alv, salv, ...) ma funzionano più o meno allo stesso modo. Per utilizzare un'alv serve un container (che dia all'alv un'estensione sullo schermo), il fieldcatalog (ovvero la descrizione della tabella che verrà mostrata) e un layout (conterrà eventuali componenti come il colore, il tipo di selezione righe e altro).

> Prima di generare la alv deve essere creato il field-catalog (vedi la pagina apposita).

```abap
DATA: r_cont TYPE REF TO cl_gui_custom_container,
      r_alv  TYPE REF TO cl_gui_alv_grid.
      
DATA: it_fcat TYPE TABLE OF lvc_s_fcat,
      wa_fcat LIKE LINE OF it_fcat.
      
 CREATE OBJECT r_cont
    EXPORTING
      container_name = 'CONT'.

  CREATE OBJECT r_alv
    EXPORTING
      i_parent = r_cont.

  CALL METHOD r_alv->set_table_for_first_display
    EXPORTING
      is_layout                     = wa_layo
    CHANGING
      it_fieldcatalog               = it_fcat
      it_outtab                     = lt_s_oda
    EXCEPTIONS
      invalid_parameter_combination = 1
      program_error                 = 2
      too_many_lines                = 3
      OTHERS                        = 4.
  IF sy-subrc <> 0.

  ENDIF.
```
Un'alv contiene degli <i>Eventi</i> che possono essere implementati nel programma locale. Gli eventi devono essere implementati attraverso un metodo Handler:
```abap
*lo_event è una classe handler
CREATE OBJECT lo_event.
SET HANDLER lo_event->handle_hotspot_click FOR r_alv.
```
Possono essere mostrate piu alv in uno stesso screen utilizzando uno splitter container.
```abap
*  Creo il contenitore che definisce l'estensione di stampa su schermo
    CREATE OBJECT lo_cont_docking
      EXPORTING
        parent = cl_gui_container=>screen0
        ratio  = 95
      EXCEPTIONS
        OTHERS = 6.

*   Imposto l'estensione della stampa su schermo
    CALL METHOD lo_cont_docking->set_extension
      EXPORTING
        extension  = 99999
      EXCEPTIONS
        cntl_error = 1
        OTHERS     = 2.

*     Creo il primo split container con parente il contenitore docking. Imposto tre righe per le tre alv utilizzate
      CREATE OBJECT lo_split_co
        EXPORTING
          parent  = lo_cont_docking
          rows    = 3
          columns = 1
          align   = 15.

*     Assegno alla prima riga del container splittato il container graphic_parent_hd -> header
      CALL METHOD lo_split_co->get_container
        EXPORTING
          row       = 1
          column    = 1
        RECEIVING
          container = graphic_parent_hd.

      CALL METHOD lo_split_co->set_row_height
        EXPORTING
          id                = 1
          height            = 4
        .
*     Assegno alla prima riga del container splittato il container graphic_parent1 -> Coil
      CALL METHOD lo_split_co->get_container
        EXPORTING
          row       = 2
          column    = 1
        RECEIVING
          container = graphic_parent1.

*     Assegno alla prima riga del container splittato il container graphic_parent2 -> Ordini
      CALL METHOD lo_split_co->get_container
        EXPORTING
          row       = 3
          column    = 1
        RECEIVING
          container = graphic_parent2.

*     Creo l'alv per i coil con parente graphic_parent1
      CREATE OBJECT lo_alv_up
        EXPORTING
          i_parent = graphic_parent1.

*     Creo l'alv per gli ordini con parente graphic_parent2
      CREATE OBJECT lo_alv_dw
        EXPORTING
          i_parent = graphic_parent2.

*     Imposto per le due alv un gestore di azioni che richiama funzioni in base al metodo chiamato
      SET HANDLER me->handle_user_command FOR lo_alv_up.
      SET HANDLER me->handle_user_command FOR lo_alv_dw.
      
      wa_layout_1-cwidth_opt   = 'X'.
      wa_layout_2-cwidth_opt  = 'X'.
      wa_layout_1-sel_mode     = 'D'.
      wa_layout_2-sel_mode    = 'D'.
      wa_layout_2-info_fname  = 'ROWCOLOR'.
      wa_layout_1-info_fname   = 'ROWCOLOR'.
      
      CALL METHOD lo_alv_up->set_table_for_first_display
        EXPORTING
          is_layout                     = wa_layout_1
          is_variant                    = lv_repname
          i_save                        = 'A'
        CHANGING
          it_fieldcatalog               = it_fcat_1[]
          it_outtab                     = out_grid_1
        EXCEPTIONS
          invalid_parameter_combination = 1
          program_error                 = 2
          too_many_lines                = 3
          OTHERS                        = 4.
      IF sy-subrc <> 0.
      ENDIF.

     CALL METHOD lo_alv_dw->set_table_for_first_display
        EXPORTING
          is_layout                     = wa_layout_2
          is_variant                    = lv_repnam2
          i_save                        = 'A'
        CHANGING
          it_fieldcatalog               = it_fcat_2
          it_outtab                     = out_grid_2
        EXCEPTIONS
          invalid_parameter_combination = 1
          program_error                 = 2
          too_many_lines                = 3
          OTHERS                        = 4.
      IF sy-subrc <> 0.
      ENDIF.
```
