# My Blog Sample - UI Moderna - React

## Aggiungere le categorie ai Post [frontend]  

Nel blog i post sono raggruppati per categorie logiche. Giacomo vorrebbe avere una pagina con l'elenco delle categorie e accedendo alla categoria siano visualizzati i Post siano contenuti all'interno della categoria. Inoltre nel dettaglio di ogni post venga visualizzata la categoria di appartenenza. Ci può essere solo una categoria per post.  

Tommaso suggerisce di modificare i dummy data dei post aggiungendo una proprietà "categoria" che contiene un oggetto con le proprietà "id" e "name".  

Inoltre suggerisce di aggiungere un nuovo file per gestire i dummy data delle categorie. Deve essere come quello per i post, ma deve trattare un oggetto che rappresenti la categoria con le proprietà id, name, description e un array con degli oggetti post.  

## Specifiche implementative
  
### Dymmy data

Modifica i dummy data dei post (*src\dummydata\posts.js*) aggiungendo una proprietà "category" che contiene un oggetto con le proprietà "id" e "name" per rappresentare una categoria.  

esempio, completata tutti i dati dei post presenti nei tuoi dummy data con dei dati delle categorie
```json
{
    "id": 3,
    "title": "Third post of the blog",
    "text": "Lorem ipsum dolor sit amet, consectetur adipiscing elit.",
    "category": {
        "id": 1,
        "name": "First category of the post",
    }
}
```

Aggiungere un nuovo file alla cartella *src\dummydata* per gestire le categorie. Deve essere come *src\dummydata\posts.js*, ma deve trattare un oggetto che rappresenti la categoria con le proprietà id, name, description e un array di post con solo le proprietà id e title.

esempio, completata tutti i dati delle categorie e aggiungi i dati dei post
```json
{
    "id": 1,
    "title": "First category of the post",
    "description": "Lorem ipsum dolor sit amet, consectetur adipiscing elit.",
    "posts": [{
        "id": 3,
        "title": "Third post of the blog"
    }]
}
```

Ricordati di importare il file di trasformazione delle categorie che creerai nei prossimi step e presta attenzione che nella funzione *getDummyDataById* il parametro passato alla filter sia un *valore intero* (se viene passata una stringa non trova corrispondenza). Usa un trucco, aggiungi un *+* davanti alla variabile questo effettua un cast ad intero.  

```javascript
dummyData.filter(item => item.id === +id);
```

### Enums

Aggiungi un file *categories.js* nella cartella *src\enums*, copia e adatta il contenuto del file *src\enums\posts.js* e rinomina le variabili e i suoi valori per trattare l'entità categoria.  

### Transformation functions

Aggiungi un file *categorie.js* nella cartella *src\transformations*, copia e adatta il contenuto del file *src\transformations\posts.js* di modo che importi il file enums relativo alle categorie.  

### Service

Aggiungi un file *CategoriesService.js* nella cartella *src\services*, copia e adatta il contenuto del file *src\services\PostsService.js* di modo che importi i file relativi alle categorie e gestisca questa entità.  

### Category pages Components

Aggiungi una nuova cartella *Categories* nella cartella *src\Components\Pages*, crea due nuovi file *List.js* e *Details.js* nella nuova cartella creata. Prendi come spunto i componenti pagina *List.js* e *Details.js* e adattali per visualizzare le categorie.  

Nel componente Details delle categorie ricordati:  
- di gestire un parametro in querystring chiamato *categoryId*  
- di visualizzare la lista dei post contenuti nella categoria  

### Post Details

Nel componente Details dei post ricordati di visualizzare il nome della categoria e, se vuoi, aggiungi un link che possa far accedere al dettaglio della categoria.  

### Categories Routing

Nella cartella *src\Components\Sections* creare un nuovo componente *CategoriesSection*, copia e adatta il componente *PostsSection* e adattalo per gestire le rotte dell'entità Category.  

- Ricordati di gestire un parametro *categoryId*.

Modifica inoltre il file *src\Components\Sections\SiteRoutes.js* importando il file creato prima e andando a gestire le rotte come viene fatto per *PostsSection*, ma rispondendo alla rotta *categories*.  

### Menù di navigazione

Crea nella cartella *src\Components\Partials* un file come *AboutSectionMenu* chiamato *BlogSectionMenu* dove andrai a gestire i link per navigare la sezione Blog (*\posts* e *\categories*).  
Vai ad includere questo componente nei file *src\Components\Pages\Categories*. Prendi spunto da come viene usato *AboutSectionMenu*.  

### Sistema i commenti per la documentazione e rigenerala

Sistema i commenti nei vari file del codice e poi rigenera la documentazione con il comando

```cmd
npm run docs
```

### Crea de test per verificare le nuove funzionalità

[TO DO]


[Ritorna alla pagina principale](../../README.md)  


