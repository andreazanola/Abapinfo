
**Select single:** estraggo solo un valore
 ```abap
SELECT SINGLE campo1, campo2 
  FROM table INTO variable
  WHERE condizione.
  
SELECT SINGLE campo1, campo2 
  FROM table INTO @DATA(variable)
  WHERE condizione.
```

**Select count:** contare le righe di una select
```abap
SELECT COUNT(*) 
  FROM table INTO variable
  WHERE condizione.
  
SELECT COUNT( DISTINT nomecampo )
  FROM table INTO variable
  WHERE   condizione.
```

**Select into table:** estraggo più valori
```abap
SELECT campo1 campo2 
  FROM table INTO TABLE tab
  WHERE condizione.
  
SELECT campo1 campo2
  FROM table INTO CORRESPONDING FIELDS OF TABLE tab
  WHERE condizione.
  
SELECT campo1 campo2
  FROM table INTO TABLE tab
  FOR ALL ENTRIES IN tab2
  WHERE condizione.
  
 SELECT campo1, campo2
  FROM table INTO TABLE @DATA(tab)
  WHERE condizione.
  
*  Nella condizione del WHERE è utilizzabile anche  '<> @( VALUE #( ) )' per indicare un valore vuoto 
```
**ATTENZIONE:**
> Per le query esistono due sintassi: la sintassi vecchia che non richiede la virgola tra i campi da selezionare, la nuova sintassi si. 
  Nella nuova sintassi deve essere inserita la chiocciola davanti alle variabili del report (quindi no campi o nomi tabella di dictionary) 
  ed è ammessa la dichiarazione inline della variabile o tabella (@DATA(nome)).  
  
> Differenza tra **INTO TABLE** e **INTO CORRESPONDING FIELD OF TABLE**. Il primo estrae dei dati e li mette nell'ordine di estrazione 
nella tabella di destinazione (quindi la tabella deve avere la struttura ordinata e con i nomi corretti), mentre nel secondo caso la 
query inserisce i valori estratti dal database nella colonna che corrisponde al dato estratto, se la colonna viene trovata.

**CASE WHEN:** https://blogs.sap.com/2013/10/05/useful-sql-with-sap-hana/
