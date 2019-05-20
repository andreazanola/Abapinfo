<b>Trasporto copie</b><br>
Per trasportare un oggetto su un altro sistema andare in <i>SE10</i> e creare una CR per il trasporto copie. Una volta creata selezionare
il box Rilevare oggetti (ctrl + f11) e inserire ciò che vuoi trasportare. Dopo aver incluso gli oggetti, impostare destinazione virtuale
VIR e rilasciarla.
<br><br>
<b>Download CR</b><br>
Lanciare la transazione <i>CG3Y</i>.<br>
Scaricare i file dai seguenti percorsi:
- \\sapdev\sap\trans\data\R(numerocr).(idsistema) 
- \\sapdev\sap\trans\cofiles\K(numerocr).(idsistema)

Questi file devono essere salvati con l'estensione (idsistema).
<br><br>
<b>Upload CR</b><br>
Lanciare la transazione <i>CG3Z</i>.<br>
Caricare i file R(numerocr).(idsistema) e K(numerocr).(idsistema) rispettivamente nelle cartelle data e cofiles del sistema d'arrivo 
<br><br>
> NB<br>
I percorsi non sono gli stessi per ogni sistema. Cercare la cartella <i>TRANS</i> tramite la transazione <i>AL11</i> per risalire alle 
due cartelle contenenti i file utili (data e cofiles).
