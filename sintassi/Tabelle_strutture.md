
```abap
" Dichiaro un tipo di struttura
TYPES: BEGIN OF ty_example,
    matnr TYPE matnr,
    mtart TYPE mtart,
    END OF ty_example.

DATA : it_example TYPE TABLE OF ty_example, " Istanzio una tabella di tipo ty_example
       wa_example TYPE ty_example.          " Istanzio una struttura di tipo ty_example
 
```
E' possibile usare 3 metodi diversi per estrarre i dati dalle tabelle:

- Utilizzando la struttura come riga della tabella
```abap
loop at it_example into wa_example.
    write:/ wa_example-matnr .
    write:/ wa_example-mtart .
endloop.
```

- Utilizzando i field-symbols come puntatori.
```abap
loop at it_example assigning field-symbol(<fs_example>).
    write:/ <fs_example>-matnr .
    write:/ <fs_example>-mtart .
endloop.
```
- Utilizzando i field-symbols come puntatori quando una tabella è dinamica (non esiste quinsi una struttura fissa ma viene generata da funzioni).
```abap
FIELD-SYMBOLS: <fs_matnr> TYPE any,
               <fs_mtart> TYPE any. " o data

loop at it_example assigning field-symbol(<fs_example>).
     ASSIGN COMPONENT 'MATNR' OF STRUCTURE <fs_example> TO <fs_matnr>.
     ASSIGN COMPONENT 'MTART' OF STRUCTURE <fs_example> TO <fs_mtart>.
    write:/ <fs_matnr> .
    write:/ <fs_mtart> .
endloop.
```
