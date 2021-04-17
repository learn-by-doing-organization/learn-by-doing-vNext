# My Simple Site Statistics - Features
([English translate](AddViews.md))  

## Aggiungere altre view di visualizzazione dati
*[database]*  
Per realizzare una dashboard dove visualizzare le statistiche degli accessi, si è notato che effettuare delle query semplici per ogni tabella è inefficiente e sarebbe utile creare delle VIEW che permettano di ottimizzare le prestazioni e di avere un dato più completo ad ogni richiesta.  

### Specifiche implementative

#### Lista delle visite per periodo di tempo (per giorno) e per sito web. Verranno visualizzati i seguenti dati: Periodo di riferimento, sito web id, sito web, numero visualizzazioni.

Per ottenere la visualizzazione delle visite per giorno e per sito web dovremo creare una VIEW che legga i dati della tabella *accesses_visits* in *JOIN* con la *accesses_pages* (che ha la relazione con la *websites*) e che effettui una *GROUP BY* per il campo *date* senza tener conto dell'ora (effettuare un *CAST* con il tipo *DATE* per eliminare l'ora) e per sito web, e che ritorni i valori *visit_date* (il campo *date* senza l'ora), *visit_website* (sia il valore dell'id del website per permettere di filtrare il risultato per website, sia il nome e l'url del website) e *num_visits* (che ritorna una *COUNT* delle visite per quella data).

Creare un sql script che inserisca la VIEW nel database (se hai bisogno di ulteriore aiuto vedi il file *003_Create_View_CompletePages.sql*).

##### Realizzare uno o più unit test che permettano di verificare il risultato della VIEW (opzionale, ma altamente consigliato)

Per validare i risultati della VIEW appena creata, realizzare uno unit test che recuperi attraverso una *JOIN* delle tabelle *accesses_visits* e *accesses_pages* il numero di visite per un dato sito web e giorno (data senza l'ora). Usa valori statici per la data della visita e il sito web, oppure recuperali randomicamente dalle rispettive tabelle.

Creare un sql script che permetta di lanciare lo unit test (se hai bisogno di ulteriore aiuto vedi il file *tests\sp_get_or_create_access_browser\should_exists.test.sql*, per verificare che effettivamente il test funzioni, rompi la VIEW in modo che torni un risultato non corretto).

#### Lista delle visite per periodo di tempo (per giorno) e per pagina, filtrate per sito web. Verranno visualizzati i seguenti dati: Periodo di riferimento, sito web id, sito web, id della pagina, url pagina, numero di visualizzazioni.

Per ottenere la visualizzazione delle visite per giorno, per pagina e per sito web dovremo creare una VIEW che legga i dati della tabella *accesses_visits* in *JOIN* con la *accesses_pages* (che ha la relazione con la *websites*) e che effettui una *GROUP BY* per il campo *date* senza tener conto dell'ora (effettuare un *CAST* con il tipo *DATE* per eliminare l'ora), per pagina e per sito web, e che ritorni i valori *visit_date* (il campo *date* senza l'ora), *visit_page* (sia il valore dell'id della pagina per permettere di filtrare il risultato per pagina, sia l'url della pagina), *visit_website* (con il valore dell'id del website per permettere di filtrare il risultato per website) e *num_visits* (che ritorna una *COUNT* delle visite per quella data).

Creare un sql script che inserisca la VIEW nel database (se hai bisogno di ulteriore aiuto vedi il file *003_Create_View_CompletePages.sql*).

##### Realizzare uno o più unit test che permettano di verificare il risultato della VIEW (opzionale, ma altamente consigliato)

Per validare i risultati della VIEW appena creata, realizzare uno unit test che recuperi attraverso una *JOIN* delle tabelle *accesses_visits* e *accesses_pages* il numero di visite per una data pagina (e quindi sito web) e giorno (data senza l'ora). Usa valori statici per la data della visita e la pagina (tenendo conto del sito web), oppure recuperali randomicamente dalle rispettive tabelle.

Creare un sql script che permetta di lanciare lo unit test (se hai bisogno di ulteriore aiuto vedi il file *tests\sp_get_or_create_access_browser\should_exists.test.sql*, per verificare che effettivamente il test funzioni, rompi la VIEW in modo che torni un risultato non corretto).

#### Lista delle visite per periodo di tempo (per giorno) e per browser, filtrate per sito web. Verranno visualizzati i seguenti dati: Periodo di riferimento, browser id, browser (user agent string), sito web id, sito web, numero di visualizzazioni.

Per ottenere la visualizzazione delle visite per giorno, per browser e per sito web dovremo creare una VIEW che legga i dati della tabella *accesses_visits* in *JOIN* con la *accesses_pages* (che ha la relazione con la *websites*), e che effettui una *GROUP BY* per il campo *date* senza tener conto dell'ora (effettuare un *CAST* con il tipo *DATE* per eliminare l'ora), per browser id e per sito web, e che ritorni i valori *visit_date* (il campo *date* senza l'ora), *visit_browser_id* (con il valore dell'id del browser per permettere di filtrare il risultato per browser e per recuperare l'user agent string), *visit_website* (sia il valore dell'id del website per permettere di filtrare il risultato per website) e *num_visits* (che ritorna una *COUNT* delle visite per quella data).

Per completare la visualizzazione di tutti i dati è necessario effettuare una SELECT con FROM la query creata sopra in INNER JOIN con la *accesses_browsers* per recuperare il valore dell'user agent string.

Creare un sql script che inserisca la VIEW nel database (se hai bisogno di ulteriore aiuto vedi il file *003_Create_View_CompletePages.sql*).

##### Realizzare uno o più unit test che permettano di verificare il risultato della VIEW (opzionale, ma altamente consigliato)

Per validare i risultati della VIEW appena creata, realizzare uno unit test che recuperi attraverso una *JOIN* delle tabelle *accesses_visits* e *accesses_browsers* il numero di visite per un dato browser e giorno (data senza l'ora). Usa valori statici per la data della visita ed il browser, oppure recuperali randomicamente dalle rispettive tabelle.

Creare un sql script che permetta di lanciare lo unit test (se hai bisogno di ulteriore aiuto vedi il file *tests\sp_get_or_create_access_browser\should_exists.test.sql*, per verificare che effettivamente il test funzioni, rompi la VIEW in modo che torni un risultato non corretto).

#### Lista delle visite per periodo di tempo (per giorno) e per utente, filtrate per sito web. Verranno visualizzati i seguenti dati: Periodo di riferimento, id utente, username, sito web id, sito web, numero di visualizzazioni.

Per ottenere la visualizzazione delle visite per giorno, per utente e per sito web dovremo creare una VIEW che legga i dati della tabella *accesses_visits* in *JOIN* con la *accesses_pages* (che ha la relazione con la *websites*) e la *users*, e che effettui una *GROUP BY* per il campo *date* senza tener conto dell'ora (effettuare un *CAST* con il tipo *DATE* per eliminare l'ora), per utente e per sito web, e che ritorni i valori *visit_date* (il campo *date* senza l'ora), *visit_user* (sia il valore dell'id dell'utente per permettere di filtrare il risultato per utente, sia l'username), *visit_website* (sia il valore dell'id del website per permettere di filtrare il risultato per website) e *num_visits* (che ritorna una *COUNT* delle visite per quella data).

Creare un sql script che inserisca la VIEW nel database (se hai bisogno di ulteriore aiuto vedi il file *003_Create_View_CompletePages.sql*).

##### Realizzare uno o più unit test che permettano di verificare il risultato della VIEW (opzionale, ma altamente consigliato)

Per validare i risultati della VIEW appena creata, realizzare uno unit test che recuperi attraverso una *JOIN* delle tabelle *accesses_visits* e *users* il numero di visite per un dato utente e giorno (data senza l'ora). Usa valori statici per la data della visita ed l-utente, oppure recuperali randomicamente dalle rispettive tabelle.

Creare un sql script che permetta di lanciare lo unit test (se hai bisogno di ulteriore aiuto vedi il file *tests\sp_get_or_create_access_browser\should_exists.test.sql*, per verificare che effettivamente il test funzioni, rompi la VIEW in modo che torni un risultato non corretto).


[Vedi il repository con l'implementazione (!!!contiene spoiler)](https://github.com/Magicianred/my-simple-site-statistics-mssql/tree/pathFromV0toV1/step01/add-views)  

[Ritorna alla pagina principale](../README_IT.md)  