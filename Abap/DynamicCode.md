<b>Subroutine pool</b> <br>
........
<br><br>
<b>Insert Report</b> <br>
Nel caso di dynpro ed enhancement, la subroutine pool è inutilizzabile. Questo metodo permette di creare un report ( o include temporaneo )
che viene richiamato all'istruzione insert report. <br>

```abap
APPEND: 'REPORT TEST' TO LT_CODE,
        'WRITE: \LV_TEST' TO LT_CODE.


INSERT REPORT 'TEST' FROM LT_CODE.
```
