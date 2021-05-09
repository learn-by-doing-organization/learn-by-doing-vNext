# My Blog Sample - UI Moderna
([English translate](README_EN.md))

## Indice

- [Prefazione](#prefazione)  
- [Istruzioni](#istruzioni)  
- [Clona il repository](#clona-il-repository)
- [Funzionalità da implementare](#funzionalità-da-implementare)  
    - [Aggiungere le categorie ai Post [frontend]](#aggiungere-le-categorie-ai-post)
        - Specifiche implementative  
        - Obbiettivi di apprendimento  
    - [Aggiungere i tag ai Post [frontend]](#aggiungere-i-tag-ai-post)
        - Specifiche implementative  
        - Obbiettivi di apprendimento  
    - [Aggiungere l'autore ai Post [frontend]](#aggiungere-l'autore-ai-post)
        - Specifiche implementative  
        - Obbiettivi di apprendimento  
    - [Aggiungere la paginazione alla lista dei Post [frontend]](#aggiungere-la-paginazione-alla-lista-dei-post)
        - Specifiche implementative  
        - Obbiettivi di apprendimento  
    - [Collegare il frontend con la web api [frontend]](#collegare-il-frontend-con-la-web-api)
        - Specifiche implementative  
        - Obbiettivi di apprendimento  

## Prefazione
Aiuta Giovanni e Tommaso a creare una moderna UI per il loro blog personale.  

Realizzazione di una Moderna UI in react per il blog di Giovanni e Tommaso ([MyBlogSample](#myblogsample)).  

Il blog è realizzato in ASP<span>.</span>NET e ha delle Rest API per alimentare l'applicativo React, ma al momento non sono pronte per cui si dovrà procedere con dei dati finti (dummy data). Questo permette di iniziare a lavorare all'applicativo frontend senza che la parte backend sia funzionante. Solo in un secondo momento, quando il backend sarà pronto, si passerà a collegarlo e vedere il sito alimentato con i dati reali.

## Istruzioni
Di seguito troverai elencate le funzionalità che si vorranno vedere implementate nel progetto. Verrà presentata una descrizione *funzionale* che è quello che il *cliente*, nel nostro caso Tommaso e Giacomo, vogliono avere sul loro blog. Se hai una certa esperienza, o vuoi metterti in gioco, questa descrizione potrebbe già bastarti per iniziare l'attività. Al contrario se hai bisogno di un aiuto per capire cosa fare clicca sul collegamento *Specifiche implementative* e troverai dei dettagli tecnici su come procedere.  

### Clona il repository
Per iniziare clona il repository del progetto

#### Repository solo React
```bash
git clone https://github.com/learn-by-doing-organization/modern-ui-react-my-blog-sample.git
```

#### Repository React + Redux *(working in progress - non ancora pronto)*
```bash
git clone https://github.com/learn-by-doing-organization/modern-ui-react-redux-my-blog-sample.git
```

## Funzionalità da implementare
Le funzionalità da implementare porteranno al rilascio della versione 1.0 del progetto.  

### Aggiungere le categorie ai Post
*[frontend]*  
Nel blog i post sono raggruppati per categorie logiche. Giacomo vorrebbe avere una pagina con l'elenco delle categorie e accedendo alla categoria siano visualizzati i Post siano contenuti all'interno della categoria. Inoltre nel dettaglio di ogni post venga visualizzata la categoria di appartenenza. Ci può essere solo una categoria per post.  

Tommaso suggerisce di modificare i dummy data dei post aggiungendo una proprietà "categoria" che contiene un oggetto con le proprietà "id" e "name".  

Inoltre suggerisce di aggiungere un nuovo file per gestire i dummy data delle categorie. Deve essere come quello per i post, ma deve trattare un oggetto che rappresenti la categoria con le proprietà id, name, description e un array con degli oggetti post.  

[Specifiche implementative React](react/Features/PostCategories.md)  
[Specifiche implementative React + Redux](react/Features/PostCategories-Redux.md)  

[Obbiettivi di apprendimento](react/LearningGoals/PostCategories.md)  

### Aggiungere i tag ai Post
*[frontend]*  
Giacomo ha saputo da un amico che lavora nel SEO che i tag sono molto comodi, quindi vuole averli anche lui nel suo blog. Come per le categorie vorrebbe una pagina con l'elenco dei tag e accedendo al tag si presenti una pagina di dettaglio con l'elenco dei post contenuti. Inoltre nella pagina di dettaglio del post si deve visualizzare l'elenco dei tag associati al post. Possono esserci zero o più tag per ogni post.  

[Specifiche implementative React](react/Features/PostTags.md)  
[Specifiche implementative React + Redux](react/Features/PostTags-Redux.md)  

[Obbiettivi di apprendimento](react/LearningGoals/PostTags.md)  

### Aggiungere l'autore ai Post
*[frontend]*  
Giacomo vorrebbe ha coinvolto altri amici per redarre i post del blog, per questo ha bisogno di visualizzare nei post chi è l'autore. Vorrebbe avere una pagina con la lista degli autori, e accedendo al dettaglio dell'autore visualizzare la lista dei post contenuti.  
L'autore è una stringa di testo e deve essere visibile nella lista dei post e nel dettaglio del post.  

[Specifiche implementative React](react/Features/PostAuthor.md)  
[Specifiche implementative React + Redux](react/Features/PostAuthor-Redux.md)  

[Obbiettivi di apprendimento](react/LearningGoals/PostAuthor.md)  

### Aggiungere la paginazione alla lista dei Post
*[frontend]*  
Giacomo già sa che il blog è ricco di post e non vuole che siano tutti visibili nella varie liste in una volta sola. Vorrebbe visualizzarli in forma paginata.  

Tommaso suggerisce di aggiungere in querystring i sue parametri necessari, uno per indicare la pagina corrente e l'altro per quanti elementi presenti in una singola pagina.  

[Specifiche implementative React](react/Features/PostPagination.md)  
[Specifiche implementative React + Redux](react/Features/PostPagination-Redux.md)  

[Obbiettivi di apprendimento](react/LearningGoals/PostPagination.md)  

### Collegare il frontend con la web api
*[frontend]*  
Giovanni e Tommasi ti avvisano che le webapi sono pronte. E' il momento di collegarle all'applicativo react.  

Questi sono gli endpoint per interrogare i dati:

[TO COMPLETE]

[Specifiche implementative React](react/Features/ConnectBackend.md)  
[Specifiche implementative React + Redux](react/Features/ConnectBackend.md)  

[Obbiettivi di apprendimento](react/LearningGoals/ConnectBackend.md)  



[Ritorna alla pagina principale](../README.md)  
