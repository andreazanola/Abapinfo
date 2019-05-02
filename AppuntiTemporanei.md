Lista oggetti in CR -> Tabella E071 E070

Scoprire che stampe utilizza un messaggio -> TNAPR 

Tab. DWINACTIV

> ------------
multiobj 

DALLA PARTITA

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
> -------------
