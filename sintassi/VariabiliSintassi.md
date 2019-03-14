**Dichiarazione variabili input** </br>

```abap
" Chiede in input un valore obbligatorio che alloca nella memoria con id wrk
PARAMETERS werks TYPE werks_d MEMORY ID wrk OBLIGATORY. 

" Chiede in input dei range 
SELECT-OPTIONS: so_kunnr FOR zstock_b-kunnr,
                so_matnr FOR zstock_b-matnr.
```

**Dichiarazione variabili interne** </br>

```abap
" Dichiaro diversi tipi di variabili seguendo la naming convention: 
" - l = local,  g = global, i = import, e = export
" - v = variable, s = structure, t = table, f = field
DATA: lv_werks TYPE werks_d,
      ls_ekko  TYPE ekko,
      lt_ekpo  TYPE TABLE OF ekpo. 

" Dichiaro un tipo struttra / tabella seguendo la naming convention:
" - ty = type, tt = type table
DATA: BEGIN OF ty_example,
      field1 type type1,
      field2 type type2,
      END OF ty_example,
      tt_example TYPE TABLE OF ty_example. " tt_example è un tipo tabella
 DATA: lt_ex TYPE tt_example. " lt_ex è quindi una tabella
      
```
