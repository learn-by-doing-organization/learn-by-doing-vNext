# My Simple Site Statistics - Features
([English translate](AddViews.md))  

## Aggiungere altre view di visualizzazione dati
*[database]*  
Per realizzare una dashboard dove visualizzare le statistiche degli accessi, si è notato che effettuare delle query semplici per ogni tabella è inefficiente e sarebbe utile creare delle VIEW che permettano di ottimizzare le prestazioni e di avere un dato più completo ad ogni richiesta.  

### Specifiche implementative

#### Lista delle visite per periodo di tempo (per giorno) e per sito web. Verranno visualizzati i seguenti dati: Periodo di riferimento, sito web, numero visualizzazioni.

Per ottenere la visualizzazione delle visite per giorno e per sito web dovremo creare una VIEW che legga i dati della tabella *accesses_visits* in *JOIN* con la *accesses_pages* (che ha la relazione con la *websites*) e che effettui una *GROUP BY* per il campo *date* senza tener conto dell'ora (effettuare un *CAST* con il tipo *DATE* per eliminare l'ora) e per sito web, e che ritorni i valori *visit_date* (il campo *date* senza l'ora), *visit_website* (con il valore dell'id del website per permettere di filtrare il risultato per website) e *num_visits* (che ritorna una *COUNT* delle visite per quella data).

Creare un sql script che inserisca la VIEW nel database (se hai bisogno di ulteriore aiuto vedi il file *003_Create_View_CompletePages.sql*).

##### Realizzare uno o più unit test che permettano di verificare il risultato della VIEW (opzionale, ma altamente consigliato)

Per validare i risultati della VIEW appena creata, realizzare uno unit test che recuperi attraverso una *JOIN* delle tabelle *accesses_visits* e *accesses_pages* il numero di visite per un dato sito web e giorno (data senza l'ora). Usa valori statici per la data della visita e il sito web, oppure recuperali randomicamente dalle rispettive tabelle.

Creare un sql script che permetta di lanciare lo unit test (se hai bisogno di ulteriore aiuto vedi il file *tests\sp_get_or_create_access_browser\should_exists.test.sql*, per verificare che effettivamente il test funzioni, rompi la VIEW in modo che torni un risultato non corretto).

#### Lista delle visite per periodo di tempo (per giorno) e per pagina, filtrate per sito web. Verranno visualizzati i seguenti dati: Periodo di riferimento, pagina visualizzata, numero di visualizzazioni.

Per ottenere la visualizzazione delle visite per giorno, per pagina e per sito web dovremo creare una VIEW che legga i dati della tabella *accesses_visits* in *JOIN* con la *accesses_pages* (che ha la relazione con la *websites*) e che effettui una *GROUP BY* per il campo *date* senza tener conto dell'ora (effettuare un *CAST* con il tipo *DATE* per eliminare l'ora), per pagina e per sito web, e che ritorni i valori *visit_date* (il campo *date* senza l'ora), *visit_page* (con il valore dell'id della pagina per permettere di filtrare il risultato per pagina), *visit_website* (con il valore dell'id del website per permettere di filtrare il risultato per website) e *num_visits* (che ritorna una *COUNT* delle visite per quella data).

Creare un sql script che inserisca la VIEW nel database (se hai bisogno di ulteriore aiuto vedi il file *003_Create_View_CompletePages.sql*).

##### Realizzare uno o più unit test che permettano di verificare il risultato della VIEW (opzionale, ma altamente consigliato)

Per validare i risultati della VIEW appena creata, realizzare uno unit test che recuperi attraverso una *JOIN* delle tabelle *accesses_visits* e *accesses_pages* il numero di visite per una data pagina (e quindi sito web) e giorno (data senza l'ora). Usa valori statici per la data della visita e la pagina (tenendo conto del sito web), oppure recuperali randomicamente dalle rispettive tabelle.

Creare un sql script che permetta di lanciare lo unit test (se hai bisogno di ulteriore aiuto vedi il file *tests\sp_get_or_create_access_browser\should_exists.test.sql*, per verificare che effettivamente il test funzioni, rompi la VIEW in modo che torni un risultato non corretto).

#### Lista delle visite per periodo di tempo (per giorno) e per browser, filtrate per sito web. Verranno visualizzati i seguenti dati: Periodo di riferimento, browser (user agent string), numero di visualizzazioni.

[TO DO]

#### Lista delle visite per periodo di tempo (per giorno) e per utente, filtrate per sito web. Verranno visualizzati i seguenti dati: Periodo di riferimento, utente, numero di visualizzazioni.

[TO DO]


[Vedi il repository con l'implementazione (!!!contiene spoiler)](https://github.com/Magicianred/my-simple-site-statistics-mssql/tree/pathFromV0toV1/step01/add-views)  

[Ritorna alla pagina principale](../README_IT.md)  