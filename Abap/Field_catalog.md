Il fieldcatalog è la tabella che contiene le proprietà dei dati che verranno stampati tramite la ALV. In questo caso il fieldcatalog viene creato dinamicamente, utilizzando il descrittore di tabelle. Siccome prende i testi dei dati dalla tabella dd04t è possibile che non tutti i campi vengano valorizzati (oppure con la presenza di più campi dello stesso tipo). In quel caso sono da inserire a mano. 

```abap
  TYPES: BEGIN OF ty_coldescr,
          rollname TYPE rollname,
          scrtext_m TYPE scrtext_m,
         END OF ty_coldescr,
         BEGIN OF ty_temp,
           field TYPE rollname,
         END OF ty_temp.

  FIELD-SYMBOLS: <fs_coldescr> TYPE ty_coldescr,
                 <fs_helpid> TYPE any,
                 <fs_comp> TYPE abap_componentdescr.
                 
DATA : ls_coldescr   TYPE ty_coldescr,
         lt_coldescr   TYPE TABLE OF ty_coldescr,
         ls_fcat       TYPE lvc_s_fcat,
         lo_ref_descr  TYPE REF TO cl_abap_structdescr,
         lr_type       TYPE REF TO cl_abap_datadescr,
         lt_comp       TYPE cl_abap_structdescr=>component_table,
         lt_temp       TYPE TABLE OF ty_temp,
         ls_temp       TYPE ty_temp.

  lo_ref_descr ?=  cl_abap_structdescr=>describe_by_name( 'ty_outtab' ).
  lt_comp = lo_ref_descr->get_components( ).

  LOOP AT lt_comp ASSIGNING <fs_comp>.
    MOVE <fs_comp>-type TO lr_type.
    
    " Assegno il campo help_id, che contiene il tipo dato
    ASSIGN lr_type->('HELP_ID') TO <fs_helpid>.
    IF <fs_helpid> IS ASSIGNED AND <fs_helpid> IS NOT INITIAL.
      MOVE <fs_helpid> TO ls_temp-field.
      APPEND ls_temp TO lt_temp.
    ENDIF.

  ENDLOOP.

" Estraggo i testi descrittori dei campi
  SELECT rollname scrtext_m
    FROM dd04t
    INTO TABLE lt_coldescr
    FOR ALL ENTRIES IN lt_temp
    WHERE rollname EQ lt_temp-field
    AND ddlanguage EQ sy-langu.

" Controllo che tutti i campi abbiano la propria descrzione -> se ci sono piu campi con stesso tipo è sempre falsa
 IF lines( lt_coldescr ) EQ lines( lt_temp ).
  LOOP AT lt_coldescr ASSIGNING <fs_coldescr>.

      ls_fcat-scrtext_m = <fs_coldescr>-scrtext_m.
      ls_fcat-datatype = <fs_coldescr>-rollname.

    APPEND ls_fcat TO gt_fcat.
    CLEAR ls_fcat.
  ENDLOOP.
ENDIF.
```
