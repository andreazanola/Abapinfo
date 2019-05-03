- DEFINE</br>

Viene utilizzato per poter utilizzare più volte le stesse righe di codice. Nei define non puoi debuggare e non possono essere utilizzati 
fuori dal programma. 

```abap
DATA: RESULT TYPE I,
      N1 TYPE I VALUE 5,
      N2 TYPE I VALUE 6.

DEFINE OPERATION.
RESULT = &1 &2 &3.
OUTPUT &1 &2 &3 RESULT.
END-OF-DEFINITION.

DEFINE OUTPUT.
WRITE: / 'The result of &1 &2 &3 is', &4.
END-OF-DEFINITION.

OPERATION 4 + 3.
OPERATION 2 ** 7.
OPERATION N2 - N1.
```

- FORM / PERFORM </br>
```abap
PERFORM OPERATION CHANGING n1 n2 tot.

FORM OPERATION CHANGING  lv_n1 TYPE i
                         lv_n2 TYPE i
                         lv_tot TYPE i.
                         
 lv_tot = lv_n1+ lv_n2.
                         
ENDFORM.
```
