    CALL FUNCTION 'UNIT_CONVERSION_SIMPLE'
      EXPORTING
        input    = slk-btgew  " Weight in LB
        unit_in  = slk-gewei  " LB
        unit_out = vttkvb-dtmeg " KG
      IMPORTING
        output   = slk-btgew. " Output : Weight in KG
        
<b>Non è possibile testarla da SE37</b>
