Leggere testi estesi.


Per inserire tutto il testo esteso in una riga: <br><br>

```abap
  CALL FUNCTION 'READ_TEXT'
  EXPORTING
    client                  = SY-MANDT         " Mandante
    id                      = <fs_txtname>-lv_id                 " ID del testo da leggere
    language                = sy-langu                  " Lingua del testo da leggere
    name                    = <fs_txtname>-lv_name                 " Nome del testo da leggere
    object                  = 'TEXT'           " Oggetto del testo da leggere
  TABLES
    lines                   = lt_text          " Righe del testo letto
  EXCEPTIONS
    id                      = 1                " ID testo non valida
    language                = 2                " Lingua non valida
    name                    = 3                " Nome testo non valido
    not_found               = 4                " Testo non trovato
    object                  = 5                " Oggetto testo non valido
    reference_check         = 6                " Catena riferimenti interrotta
    wrong_access_to_archive = 7                " Archive-Handle non consentito per l'accesso
    others                  = 8
  .

DATA(lv_text) =  REDUCE string( INIT init_text TYPE string
                               FOR ls_text IN lt_text
                               NEXT init_text = |{ init_text } { ls_text-tdline }|  ) .
```

Esiste un'alternativa alla read_text ovvero tramite estrazione da db ( <i>Vedere link esterni</i>).
