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
Giacomo vuole creare delle categorie logiche per raccogliere i Post, vorrebbe che i Post siano collegati ad una categoria, per ora non gli importa di poterli collegare a più di una categoria, ne basta una sola.  
Tommaso suggerisce di inserire una nuova tabella per le categorie e di aggiungere nella tabella dei Post un riferimento alla categoria.  

[Specifiche implementative](Features/AddViews_IT.md)  

[Obbiettivi di apprendimento](LearningGoals/AddViews_IT.md)  

### Aggiungere stored procedure di inserimento
*[database, unit test]*  
Giacomo vuole creare delle categorie logiche per raccogliere i Post, vorrebbe che i Post siano collegati ad una categoria, per ora non gli importa di poterli collegare a più di una categoria, ne basta una sola.  
Tommaso suggerisce di inserire una nuova tabella per le categorie e di aggiungere nella tabella dei Post un riferimento alla categoria.  

[Specifiche implementative](Features/AddStoredProcedures_IT.md)  

[Obbiettivi di apprendimento](LearningGoals/AddStoredProcedures_IT.md)  