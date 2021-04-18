# My Simple Site Statistics - Features
([English translate](AddStoredProcedures.md))  

### Aggiungere stored procedure di inserimento
*[database, unit test]*  
Attualmente per l'inserimento degli accessi (le visite del sito - *accesses_visites*) vengono effettuate delle INSERT sql semplici, alcune hanno bisogno prima dell'inserimento di verificare se il dato è già presente, per evitare duplicati. Questo comporta l'esecuzione di una o più interrogazioni per ogni operazione e lasciare questo compito al Backend è meno performante perché la richiesta transita dal backend al database più volte, generando traffico e ritardi. Per questo è conveniente creare una serie di stored procedure per rendere il tutto più performante.  

Potrebbe essere necessaria una sola stored procedure, quella relativa alle *accesses_visites*, ma è utile scomporla per poterla riutilizzare anche in altre parti dell'applicativo.

## Stored procedure per gli IP - *accesses_ip*

Per ottenere la stored procedure per gli IP devi avere due parametri in ingresso (l'indirizzo ip e l'hostname) e verificare con una select sulla *accesses_ips* se sono già presenti questi valori, se sì ritornare l'id del record. Se, invece, non è presente effettuare una INSERT sulla tabella e ritornare l'id appena inserito.

*Presta attenzione a verificare e "normalizzare" il parametro *hostname* (essendo una stringa può essere NULL o stringa vuota o composta di spazi) altrimenti avrai dei dati incoerenti (aiutati con il test per fare delle prove).*

##### Realizzare uno o più unit test che permettano di verificare il corretto funzionamento della Stored Procedure (opzionale, ma altamente consigliato)

Per validare i risultati della STORED PROCEDURE appena creata, realizzare almeno uno unit test che verifica il funzionamento quando i valori sono già presenti e almeno uno che verifichi quando i valori non sono presenti (e quindi è necessario effettuare l'INSERT).

Creare due sql script che permetta di lanciare gli unit test (se hai bisogno di ulteriore aiuto vedi il file *tests\sp_get_or_create_access_browser\should_exists.test.sql*, per verificare che effettivamente il test funzioni, rompi la STORED PROCEDURE in modo che torni un risultato non corretto).

## Stored procedure per le pagine - *accesses_pages*
Per ottenere la stored procedure per le pagine devi avere due parametri in ingresso (l'uri della pagina e l'id del sito web) e verificare con una SELECT sulla *accesses_pages* se sono già presenti questi valori, se sì ritornare l'id del record. Se, invece, non è presente effettuare una INSERT sulla tabella e ritornare l'id appena inserito.

##### Realizzare uno o più unit test che permettano di verificare il corretto funzionamento della Stored Procedure (opzionale, ma altamente consigliato)

Per validare i risultati della STORED PROCEDURE appena creata, realizzare almeno uno unit test che verifica il funzionamento quando i valori sono già presenti e almeno uno che verifichi quando i valori non sono presenti (e quindi è necessario effettuare l'INSERT).

*Presta attenzione che nello unit test che verifica l'inserimento devi generare random una stringa da passare come parametro per l'indirizzo della pagina.*

Creare due sql script che permetta di lanciare gli unit test (se hai bisogno di ulteriore aiuto vedi il file *tests\sp_get_or_create_access_browser\should_exists.test.sql*, per verificare che effettivamente il test funzioni, rompi la STORED PROCEDURE in modo che torni un risultato non corretto).

## Stored procedure per le visite - *accesses_visites* 
Per ottenere la stored procedure per le visite devi avere cinque parametri in ingresso (l'uri della pagina, l'url referer, l'user agent, l'id dell'utente e l'id del sito web).

Devi richiamare le stored procedure create in precedenza, quella per inserire le pagine (per il parametro url e url referer) e quella per l'user agent. Con il ritorno delle stored procedure chiamate e l'id utente e l'id del sito web puoi effettuare una INSERT nella tabella *accesses_visits*


[Vedi il repository con l'implementazione (!!!contiene spoiler)](https://github.com/Magicianred/my-simple-site-statistics-mssql/tree/pathFromV0toV1/step02/add-stored-procedures)  

[Ritorna alla pagina principale](../README_IT.md)  

