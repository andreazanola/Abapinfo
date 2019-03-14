Per poter ottenere la struttura di una tabella interna (nome e tipo delle colonne), è possibile utilizzare delle classi che aiutano l'estrazione di queste informazioni.

```abap

  "mapping partner
  DATA : lo_ref_descr TYPE REF TO cl_abap_structdescr,
         lt_detail   TYPE abap_compdescr_tab,
         ls_detail   LIKE LINE OF lt_detail,
         ls_c_compcd TYPE idwtcompcd.

  lo_ref_descr ?= cl_abap_typedescr=>describe_by_data( ls_c_compcd ). "Chiamare metodo statico su una struttura
  lt_detail[] = lo_ref_descr->components. "Dammi le colonne

  LOOP AT lt_detail INTO ls_detail.
    "Qui ho le colonne della tabella
  ENDLOOP.
  
```
