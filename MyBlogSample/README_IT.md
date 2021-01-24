# My Blog Sample - Versione 1
([English translate](README.md))

## Indice

- [Prefazione](#prefazione)
- [Versione 0](#versione-0)
- [Versione 1](#versione-1) - (in corso di sviluppo)
    - [Miglioramento UI e alcune funzionalità](#miglioramento-ui-e-alcune-funzionalità)
    - [Creazione sezione amministrativa](#creazione-sezione-amministrativa)
    - [Miglioramento web api](#miglioramento-web-api)
    - [Statistiche accesso sito](#statistiche-accesso-sito)
    - [Crezione UI moderna](#creazione-ui-moderna)

## Prefazione
Giacomo e Tommaso sono due amici che hanno deciso di fare un blog.  
Giacomo è sempre pieno di idee e ha coinvolto Tommaso, che è un programmatore sempre troppo impegnato, nella realizzazione di questo progetto personale. 

## Versione 0 

Tommaso voleva aiutare il suo amico, ma avendo poco tempo ha lasciato a metà il progetto.  
Giacomo non si è però scoraggiato e con una delle sue idee ha trovato il modo di portare comunque avanti il progetto: cercando in rete ti ha trovato e ti ha chiesto aiuto per il suo blog, sa che non sei un esperto programmatore, ma con alcune indicazioni di Tommaso su come procedere non ci sarà nessun problema!  

Il codice del progetto è molto strutturato, ma ha ancora poche funzionalità, è predisposto per i test, ma quelli attuali non hanno molto senso, ma sono in ogni caso un'ottima base per crearne di nuovi. 

[Scopri di più](version0/README_IT.md)  

## Versione 1
[In corso di sviluppo]

Tommaso è entusiasta del rilascio della versione 1 del blog ed è già pieno di idee per i prossimi sviluppi!  

### Miglioramento UI e alcune funzionalità
*[backend, frontend]*  

In attesa della nuova UI moderna, Giovanni vorrebbe fare alcune miglioramenti all'attuale UI e aggiungere alcune funzionalità, come la possibilità di commentare.

Tommaso ha già preparato un sistema di accessi per permettere ai singoli utenti del blog di loggarsi e permettere di essere autenticati.  

[Scopri di più](version1/01_improvement-ui/README_IT.md)  

### Creazione sezione amministrativa
*[database, backend, frontend]*  

Ora che il blog è a regime e ci sono diversi autori dei post è necessario permettere di inserire i post attraverso un'interfaccia web: una sezione amministrativa ad accesso riservato!  

Tommaso ha già preparato un sistema di accessi per permettere ai singoli autori del blog di loggarsi e gestire i propri post, ma ha bisogno di una mano per completare il crud (create/read/update/delete) di tutte le entità. Per farlo si utilizzerà lo scaffolding di dotnet.  

[Scopri di più](version1/02_admin_section/README_IT.md)  

### Miglioramento web api
*[database, backend]*  

Nella versione 0 del progetto era già presente una rudimentale web api, ma non veniva usata. Ora che si prevede la realizzazione di una moderna UI è fondamentale avere una web api efficiente che rispetti il modello REST.  

Tommaso ha già preparato un sistema di accessi per permettere agli utenti di avere una loro login e password ed ottenere un token di accesso.  

[Scopri di più](version1/03_web_api/README_IT.md)    

### Statistiche accesso sito
*[database]*  

Giovanni vorrebbe avere un modo per registrare gli accessi al blog e poterli visualizzare così da sapere quante persone seguono giornalmente, settimanalmente e mensilmente il suo blog.  

Tommaso ha già pensato che saranno necessarie diverse tabelle per immagazzinare i dati, alcune stored procedure per inserirli e delle viste per facilitare la visualizzazione, ma sa che non avrà il tempo di realizzarlo. Per questo Giovanni ha consultato il suo network ed ha scoperto che Marco, un collega di Tommaso, sta realizzando un sistema per fare questo e sta seguendo gli sviluppi del suo progetto!  

[Scopri di più](../MySimpleSiteStatistics/README_IT.md)  

### Creazione UI moderna
*[frontend]*  

Molti utenti si sono lamentati dell'attuale UI che è poco reattiva e molto "old-style", per questo Tommaso ha suggerito di preparare un frontend con una tecnologia più moderna che permetta di visualizzare i dati e leggere e ricercare i vari post senza dover ricaricare ogni volta tutta la pagina.

Tommaso ha chiesto a colleghi ed amici se qualcuno volesse fare questa parte e ha scoperto che Veronica, una sua amica che fa frontend, può dargli una mano.  

[Scopri di più (versione in React)](../MyBlogSample-ModernUI/react/README_IT.md)  
