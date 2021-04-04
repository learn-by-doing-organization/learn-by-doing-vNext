# My Simple Site Statistics
([English translate](README.md))

## Indice

- [Prefazione](#prefazione)  
- [Istruzioni](#istruzioni)  
- [Clona il repository](#clona-il-repository)
- [Funzionalità da implementare](#funzionalità-da-implementare)  
    - [Aggiungere altre view di visualizzazione dati [database]](#aggiungere-altre-view-di-visualizzazione-dati)
    - [Aggiungere altre stored procedure di inserimento [database, unit test]](#aggiungere-stored-procedure-di-inserimento)

## Prefazione  

Marco sta sviluppando un sistema per registrare gli accessi ai siti web.  
Per realizzarlo ha creato diverse tabelle per immagazzinare i dati, alcune stored procedure per inserirli e delle viste per facilitare la visualizzazione.  

Giacomo, un collega di Tommaso, si è dimostrato interessato al progetto e ha chiesto una serie di funzionalità da aggiungere al progetto per implementarlo nel proprio blog e avere finalmente un modo per sapere quanti accessi riceve il proprio sito.  

Marco, vista l'inaspettata richiesta di funzionalità ha bisogno di una mano, Giacomo gli ha suggerito il tuo nome e ora Marco ti ha chiesto di implementare alcune delle funzionalità.

## Istruzioni
Di seguito troverai elencate le funzionalità che si vorranno vedere implementate nel progetto. Verrà presentata una descrizione *funzionale* che è quello che il *cliente*, nel nostro caso Giacomo, vuole avere sul suo blog. Se hai una certa esperienza, o vuoi metterti in gioco, questa descrizione potrebbe già bastarti per iniziare l'attività. Al contrario se hai bisogno di un aiuto per capire cosa fare clicca sul collegamento *Specifiche implementative* e troverai dei dettagli tecnici su come procedere.  

### Clona il repository
Per iniziare clona il repository del progetto

```bash
git clone https://github.com/Magicianred/my-simple-site-statistics-mssql.git
```

## Funzionalità da implementare
Le funzionalità da implementare porteranno al rilascio della versione 1.0 del progetto.  

### Aggiungere altre view di visualizzazione dati
*[database]*  
Per realizzare una dashboard dove visualizzare le statistiche degli accessi, si è notato che effettuare delle query semplici per ogni tabella è inefficiente e sarebbe utile creare delle VIEW che permettano di ottimizzare le prestazioni e di avere un dato più completo ad ogni richiesta.  

La dashboard presenterà queste statistiche:
- Lista delle visite per periodo di tempo (per giorno) e per sito web. Verranno visualizzati i seguenti dati: Periodo di riferimento, sito web, numero visualizzazioni.
- Lista delle visite per periodo di tempo (per giorno) e per pagina, filtrate per sito web. Verranno visualizzati i seguenti dati: Periodo di riferimento, pagina visualizzata, numero di visualizzazioni.
- Lista delle visite per periodo di tempo (per giorno) e per browser, filtrate per sito web. Verranno visualizzati i seguenti dati: Periodo di riferimento, browser (user agent string), numero di visualizzazioni.
- Lista delle visite per periodo di tempo (per giorno) e per utente, filtrate per sito web. Verranno visualizzati i seguenti dati: Periodo di riferimento, utente, numero di visualizzazioni.

[Specifiche implementative](Features/AddViews_IT.md)  

[Obbiettivi di apprendimento](LearningGoals/AddViews_IT.md)  

### Aggiungere stored procedure di inserimento
*[database, unit test]*  
Attualmente per l'inserimento degli accessi (le visite del sito - *accesses_visites*) vengono effettuate delle INSERT sql semplici, alcune hanno bisogno prima dell'inserimento di verificare se il dato è già presente, per evitare duplicati. Questo comporta l'esecuzione di una o più interrogazioni per ogni operazione e lasciare questo compito al Backend è meno performante perché la richiesta transita dal backend al database più volte, generando traffico e ritardi. Per questo è conveniente creare una serie di stored procedure per rendere il tutto più performante.  

Potrebbe essere necessaria una sola stored procedure, quella relativa alle *accesses_visites*, ma è utile scomporla per poterla riutilizzare anche in altre parti dell'applicativo.

Oltre a quella già presente, per inserire gli *accesses_browser*, è necessario creare le seguenti:

- *accesses_ip*
- *accesses_pages* (che deve verificare anche il web_sites di riferimento)
- *accesses_visites* (che deve verificare le pagine, quella corrente e la referrer, il browser e l'utente)

[Specifiche implementative](Features/AddStoredProcedures_IT.md)  

[Obbiettivi di apprendimento](LearningGoals/AddStoredProcedures_IT.md)  

