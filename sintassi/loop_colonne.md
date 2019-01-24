```abap
DATA : it_mara TYPE STANDARD TABLE OF mara  WITH HEADER LINE.
 
DATA : it_detail   TYPE abap_compdescr_tab,
           wa_comp TYPE abap_compdescr.
 
DATA : ref_descr TYPE REF TO cl_abap_structdescr.
 
ref_descr ?= cl_abap_typedescr=>describe_by_data( it_mara ).
it_detail[] = ref_descr->components .
 
loop at it_detail into wa_comp.
write:/ wa_comp-name .
endloop.
```