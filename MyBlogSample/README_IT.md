# My Blog Sample
([English translate](README.md))

## Indice

- [Prefazione](#prefazione)  
- [Istruzioni](#istruzioni)  
- [Funzionalità da implementare](#funzionalità-da-implementare)  
    - [Aggiungere le categorie ai Post [database, backend, frontend]](#aggiungere-le-categorie-ai-post)
        - [Specifiche implementative](Features/PostCategories_IT.md) 
        - [Obbiettivi di apprendimento](LearningGoals/PostCategories_IT.md)  
    - [Aggiungere i tag ai Post [database, backend, frontend]](#aggiungere-i-tag-ai-post)
        - [Specifiche implementative](Features/PostTags_IT.md) 
        - [Obbiettivi di apprendimento](LearningGoals/PostTags_IT.md)  
    - [Aggiungere l'autore ai Post [database, backend, frontend]](#aggiungere-l'autore-ai-post)
        - [Specifiche implementative](Features/PostAuthor_IT.md) 
        - [Obbiettivi di apprendimento](LearningGoals/PostAuthor_IT.md)  
    - [Aggiungere la paginazione alla lista dei Post [database, backend, frontend]](#aggiungere-la-paginazione-alla-lista-dei-post)
        - [Specifiche implementative](Features/PostPagination_IT.md) 
        - [Obbiettivi di apprendimento](LearningGoals/PostPagination_IT.md)  
    - [Test manuali e correzioni di bug noti [backend, frontend, testing]](#test-manuali-e-correzioni-di-bug-noti)
        - [Specifiche implementative](Features/TestingAndBugFixing_IT.md) 
        - [Obbiettivi di apprendimento](LearningGoals/TestingAndBugFixing_IT.md)  
- [Nice To Have (NTH)](#nice-to-have-(nth))  
    - [Una nuova User Interface (UI) [frontend]](#una-nuova-user-interface-(ui))  
    - [Utilizzo di un framework moderno per il frontend [frontend+javascript]](#utilizzo-di-un-framework-moderno-per-il-frontend)  

## Prefazione
Giacomo e Tommaso sono due amici che hanno deciso di fare un blog.  
Giacomo è sempre pieno di idee e ha coinvolto Tommaso, che è un programmatore sempre troppo impegnato, nella realizzazione di questo progetto personale.  

Tommaso voleva aiutare il suo amico, ma avendo poco tempo ha lasciato a metà il progetto.  
Giacomo non si è però scoraggiato e con una delle sue idee ha trovato il modo di portare comunque avanti il progetto: cercando in rete ti ha trovato e ti ha chiesto aiuto per il suo blog, sa che non sei un esperto programmatore, ma con alcune indicazioni di Tommaso su come procedere non ci sarà nessun problema!  

Il codice del progetto è molto strutturato, ma ha ancora poche funzionalità, è predisposto per i test, ma quelli attuali non hanno molto senso, ma sono in ogni caso un'ottima base per crearne di nuovi.  

## Istruzioni
Di seguito troverai elencate le funzionalità che si vorranno vedere implementate nel progetto. Verrà presentata una descrizione *funzionale* che è quello che il *cliente*, nel nostro caso Tommaso e Giacomo, vogliono avere sul loro blog. Se hai una certa esperienza, o vuoi metterti in gioco, questa descrizione potrebbe già bastarti per iniziare l'attività. Al contrario se hai bisogno di un aiuto per capire cosa fare clicca sul collegamento *Specifiche implementative* e troverai dei dettagli tecnici su come procedere.  

## Funzionalità da implementare
Le funzionalità da implementare porteranno al rilascio della versione 2.0 del progetto.  

### Aggiungere le categorie ai Post
*[database, backend, frontend]*  
Giacomo vuole creare delle categorie logiche per raccogliere i Post, vorrebbe che i Post siano collegati ad una categoria, per ora non gli importa di poterli collegare a più di una categoria, ne basta una sola.  
Tommaso suggerisce di inserire una nuova tabella per le categorie e di aggiungere nella tabella dei Post un riferimento alla categoria.  

[Specifiche implementative](Features/PostCategories_IT.md)  

[Obbiettivi di apprendimento](LearningGoals/PostCategories_IT.md)  

### Aggiungere i tag ai Post
*[database, backend, frontend]*  
Giacomo ha saputo da un amico che lavora nel SEO che i tag sono molto comodi, quindi vuole averli anche lui nel suo blog.  

Tommaso suggerisce di creare una nuova tabella per i Tag e di creare una tabella di relazione con la tabella dei Post.  

[Specifiche implementative](Features/PostTags_IT.md)  

[Obbiettivi di apprendimento](LearningGoals/PostTags_IT.md)  

### Aggiungere l'autore ai Post
*[database, backend, frontend]*  
Giacomo vorrebbe coinvoltere altri amici per redarre i post del blog, per questo ha bisogno di indicare nei post chi è l'autore. Al momento non pensa sia necessario creare l'entità Autori, basterà solo indicare l'autore.  
Inoltre avrebbe piacere che si possa avere una lista dei post di uno specifico autore.  

Tommaso suggerisce di aggiungere un campo Autore nella tabella dei Post e di passare un parametro in querystring per filtrare la lista dei post.  

[Specifiche implementative](Features/PostAuthor_IT.md)  

[Obbiettivi di apprendimento](LearningGoals/PostAuthor_IT.md)  

### Aggiungere la paginazione alla lista dei Post
*[database, backend, frontend]*  
Giacomo già sa che il blog si riempirà presto di post e non vuole che siano tutti visibili nella home page in una volta sola. Vorrebbe visualizzarli in forma paginata sia sulla home che nel dettaglio della categoria e dei tag. Inoltre anche i tag e le categorie andranno paginate.    

Tommaso suggerisce di aggiungere la paginazione alla action *Index* del controller *HomeController* per permettere di visualizzare solo 3 posto alla volta. Verranno passati due parametri in querystring, uno per il numero di pagina, l'altro per indicare quanti elementi visualizzare in ogni pagina. Stessa cosa per le altre action che vanno paginate.  

[Specifiche implementative](Features/PostPagination_IT.md)  

[Obbiettivi di apprendimento](LearningGoals/PostPagination_IT.md)  

### Test manuali e correzioni di bug noti
*[backend, frontend, testing]*  
Giovanni ha chiesto a Tommaso di dare un'occhiata al sito perché sembra ci siano dei problemi.  

Tommaso si è reso conto di aver modificato la UI del progetto Web, ma di non aver sistemato il test *should_retrieve_all_posts* del progetto *Magicianred.LearnByDoing.MyBlog.Web.Tests.Integration* che ora riporta un errore.  
Inoltre è stato segnalato un errore nel recupero dei post per tag. Sembra che vengano recuperati sempre tutti i post, bisogna verificare e risolvere il problema.  
Tommaso ti ha chiesto inoltre di dargli una mano per vericare l'esistenza di altri bug. Se ne trovi qualcuno segnalo su GitHub e, poi se vuoi, dai una mano a risolverlo.  

[Specifiche implementative](Features/TestingAndBugFixing_IT.md)  

[Obbiettivi di apprendimento](LearningGoals/TestingAndBugFixing_IT.md)  

## Nice To Have (NTH)
Le funzionalità NTH non sono previste nel rilascio della versione 1.0 del progetto, ma saranno probabilmente implementate nella versione 2.0.  

### Una nuova User Interface (UI)
*[frontend]*  
Giacomo sente la necessità, su richiesti anche di molti frequentatori del blog, di avere una migliore UI per la fruzione del blog. Qualcosa di più "bello", "moderno" ed "accattivante".

### Utilizzo di un framework moderno per il frontend
*[frontend+javascript]*  
Giacomo ha visitato il blog di amici e ha visto che utilizzano delle tecniche di visualizzazione del frontend più dinamiche. Non c'è necessità di ricaricare la pagina ad ogni click e tutto sembra più fluido, come fosse un'applicazione Desktop. Tommaso ha spiegato a Giacomo che serve introdurre un framework moderno per visualizzare l'interfaccia e migliorare le web api che attualmente sono presenti nell'applicativo.

