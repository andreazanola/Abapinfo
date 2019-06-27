<b>Subroutine pool</b> <br>
........
<br><br>


<b>Insert Report</b> <br>
Crea a sistema un report partendo da un codice generato dinamicamente. 
```abap
APPEND: 'REPORT TEST' TO LT_CODE,
        'WRITE: \LV_TEST' TO LT_CODE.


INSERT REPORT 'TEST' FROM LT_CODE.
```
<br><br><br>
<i>Vedere link esterni per approfondimanto</i>
