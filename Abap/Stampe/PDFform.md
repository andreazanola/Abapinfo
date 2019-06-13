**Interfaccia**</br>
Nell'interfaccia vengono dichiarate le variabili di passaggio tra il report e il modulo. Qui, le variabili possono essere ulteriormente lavorate (meglio di no) per passare dati diversi da quelli provenienti dal report.

**Modulo** </br>
Il modulo della stampa PDF contiene il layout grafico che consente, tramite moduli e oggetti, di creare un documento organizzato con le variabili ricevute dall'interfaccia. Le variabili vengono connesse quindi agli oggetti attraverso il binding. 
Nel modulo è possibile inserire degli script in javascript e formcalc (fortemente sconsigliati, funzionano male e sono di difficile gestione). Nella sezione di passaggio variabili dall'interfaccia al modulo possono essere disattivate le variabili non utilizzate. E' inoltre possibile utilizzare "oggetti" specifici (tipo l'oggetto indirizzo) per delle formattazioni specifiche di determinate informazioni
- Logo
  - https://blogs.sap.com/2014/06/09/how-to-place-an-se78-image-on-an-adobe-form/
    
**Report**</br>
Nel report viene inserito il codice di estrazione e lavorazione dei dati. Una volta lavorati i dati vengono chiamate le function di open e close job.

 ```abap
  DATA: lv_fm_name   TYPE rs38l_fnam,
        ls_outpar    TYPE sfpoutputparams,
        lv_xstring   TYPE xstring.
        
 " Ottengo il logo per l'etichetta
    CALL METHOD cl_ssf_xsf_utilities=>get_bds_graphic_as_bmp
      EXPORTING
        p_object       = 'GRAPHICS'
        p_name         = 'ZF_HEADER'
        p_id           = 'BMAP'
        p_btype        = 'BCOL'
      RECEIVING
        p_bmp          = lv_xstring
      EXCEPTIONS
        not_found      = 1
        internal_error = 2
        OTHERS         = 3.
        
    " Provo a leggere il nome del function module
    TRY .
        CALL FUNCTION 'FP_FUNCTION_MODULE_NAME'
          EXPORTING
            i_name     = 'ZFM_NOME'
          IMPORTING
            e_funcname = lv_fm_name.

    ENDTRY.

    CALL FUNCTION 'FP_JOB_OPEN'
      CHANGING
        ie_outputparams = ls_outpar
      EXCEPTIONS
        cancel          = 1
        usage_error     = 2
        system_error    = 3
        internal_error  = 4
        OTHERS          = 5.

    CALL FUNCTION lv_fm_name
      EXPORTING
        is_printdata   = ls_printdata " Struttura che passo
        ix_logo        = lv_xstring " Logo che passo
      EXCEPTIONS
        usage_error    = 1
        system_error   = 2
        internal_error = 3
        OTHERS         = 4.


    CALL FUNCTION 'FP_JOB_CLOSE'
      EXCEPTIONS
        usage_error    = 1
        system_error   = 2
        internal_error = 3
        OTHERS         = 4.
 ```
 
La stampa viene lanciata con un messaggio specifico. I vari dati di questo messaggio sono contenuti nella struttura <i>NAST</i>.
