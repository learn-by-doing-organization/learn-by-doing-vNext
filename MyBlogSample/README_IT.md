# My Blog Sample  

## Prefazione  
Giacomo e Tommaso sono due amici che hanno deciso di fare un blog.  
Giacomo è sempre pieno di idee e ha coinvolto Tommaso, che è un programmatore sempre troppo impegnato, nella realizzazione di questo progetto personale.  

Tommaso voleva aiutare il suo amico, ma avendo poco tempo ha lasciato a metà il progetto.  
Giacomo non si è però scoraggiato e con una delle sue idee ha trovato il modo di portare comunque avanti il progetto: cercando in rete ti ha trovato e ti ha chiesto aiuto per il suo blog, sa che non sei un esperto programmatore, ma con alcune indicazioni di Tommaso su come procedere non ci sarà nessun problema!  

Il codice del progetto è molto strutturato, ma ha ancora poche funzionalità, è predisposto per i test, ma quelli attuali non hanno molto senso, ma sono in ogni caso un'ottima base per crearne di nuovi.  

## Funzionalità da implementare  
Le funzionalità da implementare porteranno al rilascio della versione 2.0 del progetto.  

### Aggiungere le categorie ai Post [database, backend, frontend]
Giacomo vuole creare delle categorie logiche per raccogliere i Post, vorrebbe che i Post siano collegati ad una categoria, per ora non gli importa di poterli collegare a più di una categoria, ne basta una sola.  
Tommaso suggerisce di inserire una nuova tabella per le categorie e di aggiungere nella tabella dei Post un riferimento alla categoria.  

(Specifiche implementative)[Features/PostCategories_IT.md]  

### Aggiungere i tag ai Post [database, backend, frontend]
Giacomo ha saputo da un amico che lavora nel SEO che i tag sono molto comodi, quindi vuole averli anche lui nel suo blog.  
Tommaso suggerisce di creare una nuova tabella per i Tag e di creare una tabella di relazione con la tabella dei Post.  

(Specifiche implementative)[Features/PostTags_IT.md]  

### Aggiungere l'autore ai Post [database, backend, frontend]  
Giacomo vorrebbe coinvoltere altri amici per redarre i post del blog, per questo ha bisogno di indicare nei post chi è l'autore. Al momento non pensa sia necessario creare l'entità Autori, basterà solo indicare l'autore.  
Tommaso suggerisce di aggiungere un campo Autore nella tabella dei Post.  

(Specifiche implementative)[Features/PostAuthor_IT.md]  

### Aggiungere la paginazione alla lista dei Post [backend, frontend]  
Giacomo sa già che il blog sarà ricco di post e non vuole che siano tutti visibili nella prima pagina.  
Tommaso suggerisce di inserire la paginazione alla action *Index* del controller *HomeController* che permetta di visualizzare solo 3 post alla volta.  

(Specifiche implementative)[Features/PostPagination_IT.md]  

### Correggere il test [backend, testing]
Tommaso si è reso conto di aver modificato la UI del progetto Web, ma non aver sistemato il test *should_retrieve_all_posts* del progetto *Magicianred.LearnByDoing.MyBlog.Web.Tests.Integration* che ho riporta un errore.  

(Specifiche implementative)[Features/ErrorInTest_IT.md]  

## Nice To Have (NTH)
Le funzionalità NTH non sono previste nel rilascio della versione 2.0 del progetto, ma saranno probabilmente implementate nella versione 3.0.  

### Una nuova User Interface [frontend]

(Specifiche implementative)[Features/NewUI_IT.md]  

### Utilizzo di un framework moderno per il frontend [frontend+javascript]

(Specifiche implementative)[Features/ClientFramework_IT.md]  
