Capita si debba sollevare un evento in modo statico da codice (da una badi o da un'altro metodo). Si deve ricorrere quindi ad una classe
standard per fare il RAISE.

```abap
 DATA : lv_objtype          TYPE sibftypeid VALUE 'ZCL_UD_UPDATE_QUARTA3_IDOC',
         lv_event            TYPE sibfevent VALUE 'CREATE_IDOC',
         lv_param_name       TYPE swfdname,
         wf_objkey           TYPE sweinstcou-objkey,
         lr_event_parameters TYPE REF TO if_swf_ifs_parameter_container.

  " Chiamo il metodo della classe per ottenere un container dell'evento
  CALL METHOD cl_swf_evt_event=>get_event_container
    EXPORTING
      im_objcateg  = cl_swf_evt_event=>mc_objcateg_cl
      im_objtype   = lv_objtype
      im_event     = lv_event
    RECEIVING
      re_reference = lr_event_parameters. " Parametri dell'evento che si vuole chiamare

  " Setto i parametri dell'evento che voglio chiamare
  TRY.
      lr_event_parameters->set(
        EXPORTING
          name                          = 'I_LOTTO'
          value                         = new_insplot
      ).

    CATCH cx_swf_cnt_cont_access_denied.    "
    CATCH cx_swf_cnt_elem_access_denied.    "
    CATCH cx_swf_cnt_elem_not_found.    "
    CATCH cx_swf_cnt_elem_type_conflict.    "
    CATCH cx_swf_cnt_unit_type_conflict.    "
    CATCH cx_swf_cnt_elem_def_invalid.    "
    CATCH cx_swf_cnt_container.    "
  ENDTRY.

  " Sollevo l'evento
  try.
        call method cl_swf_evt_event=>raise_in_update_task
          exporting
            im_objcateg        = cl_swf_evt_event=>mc_objcateg_cl
            im_objtype         = lv_objtype
            im_event           = lv_event
            im_objkey          = wf_objkey
            im_event_container = lr_event_parameters.
      catch cx_swf_evt_invalid_objtype .
      catch cx_swf_evt_invalid_event .
    endtry.
```
<br>
<br>
<b>Attenzione:</b><br>
Il RAISE non è obbligatorio farlo scattare con il metodo <i>raise_in_update_task</i> ma dipende dal fattore di sincronizzazione del raise
