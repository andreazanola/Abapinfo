La dynpro è la combinazione della logica e della view. Possiede dei moduli per la gestione di input (PAI) e di output (PBO). In questi moduli è possibile inserire del codice custom per modificare a piacimento dati o comportamenti di determinati elementi. La dynpro è identificata da un numero di 4 cifre e viene chiamata dal report tramite la chiamata <i>CALL SCREEN XXXX</i>.

**PAI** </br>
Vengono gestiti i dati di input, estratti nuovi dati, ecc... Qui possono essere modificati i valori mostrati a schermo. Per far si che lo schermo rimanga ggiornato inserire il metodo <i>cl_gui_cfw=>set_new_ok_code( new_code = 'REFR' )</i> alla fine del modulo, affinchè lo schermo venga aggiornato.

**PBO**</br>
In questo modulo è possibile nascondere o mostrare i vari elementi contenuti nella dynpro. E' infatti possibile ciclare sui vari elementi tramite il <i>LOOP AT SCREEN</i> e vedere il nome (o il gruppo) dell'elemento stampato (questo riguarda solo gli elementi creati tramite layout della dynpro, non coinvolge cose nell'alv).

