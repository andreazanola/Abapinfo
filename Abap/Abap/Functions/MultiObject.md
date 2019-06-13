Il metodo multiobj della classe reg viene utilizzato per l'estrazione delle caratteristiche. In base alle caratteristiche da estrarre si utilizzano varie combinazioni di accesso al metodo.</br>
In input riceve:
- r_object: gli oggetti di cui estrarre le caratteristiche
- r_char_filt: sono le caratteristiche da filtrare
- r_char_to_read: sono le caratteristiche che vogliamo leggere
- i_clastype: classe dell'oggetto da leggere
- i_directtable ??
</br>
In output restituisce:
- et_values_char: valori delle caratteristiche tipo CHAR
- et_values_num: valori delle caratteristiche tipo NUM
- et_objects: oggetti di cui abbiamo estratto le caratteristiche
-eto_tab_w_char

Esempio del codice:
```abap
    
    " Tabelle da utilizzare
    DATA: lt_objects_mtnr     TYPE TABLE OF clsel_search_objects,
          lt_num              TYPE TABLE OF /reg/_alloc_values_num,
          LT_BATCH_FILTER     type /REG/_TYT_CHARS_VAL,
          lt_char             TYPE TABLE OF /reg/_alloc_values_char,
          
    " Per le caratteristiche del materiale
    ls_objects-object(18) = ls_mara-matnr.
    ls_objects-object+18(10) = ls_mara-posnr.
    TRY.
        CALL METHOD /reg/cl_clas=>multiobj_getcfg
          EXPORTING
            r_object       = lt_objects_mtnr
            r_char_filt    = lt_batch_filter
            r_char_to_read = lt_char_read_batch
            i_clastype     = '023'
            i_directtable  = 'X'
          IMPORTING
            et_values_char = lt_char[]
            et_values_num  = lt_num[]
            et_objects     = lt_objects_mtnr
            eto_tab_w_char = lt_tab_char.
      CATCH zcx_orc.

    ENDTRY.
    
 " Per le caratteristiche della partita
 ls_objects-object(18) = ls_mch1-matnr.
 ls_objects-object+18(10) = ls_mch1-charg.
 ls_objects-cuobj = ls_mch1-cuobj_bm.
 CALL METHOD /reg/cl_clas=>multiobj_getcfg
          EXPORTING
            r_object       = lt_objects[]
            r_char_to_read = lt_char_2br[]
            i_objecttable  = 'MCH1'
            i_clastype     = '023'
            i_directtable  = 'X'
          IMPORTING
            et_values_char = lt_char[].

```

