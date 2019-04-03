```abap
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

    ASSIGN lr_type->('HELP_ID') TO <fs_helpid>.
    IF <fs_helpid> IS ASSIGNED AND <fs_helpid> IS NOT INITIAL.
      MOVE <fs_helpid> TO ls_temp-field.
      APPEND ls_temp TO lt_temp.
    ENDIF.

  ENDLOOP.

  SELECT rollname ddtext
    FROM dd04t
    INTO TABLE lt_coldescr
    FOR ALL ENTRIES IN lt_temp
    WHERE rollname EQ lt_temp-field
    AND ddlanguage EQ sy-langu.

 IF lines( lt_coldescr ) EQ lines( lt_temp ).
  LOOP AT lt_coldescr ASSIGNING <fs_coldescr>.

      ls_fcat-scrtext_m = <fs_coldescr>-ddtext.
      ls_fcat-datatype = <fs_coldescr>-rollname.

    APPEND ls_fcat TO gt_fcat.
    CLEAR ls_fcat.
  ENDLOOP.
ENDIF.
```
