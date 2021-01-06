# My Blog Sample
([English translate](PostPagination.md))  

## Aggiungere la paginazione alla lista dei Post [database, backend, frontend]
Giacomo già sa che il blog si riempirà presto di post e non vuole che siano tutti visibili nella home page in una volta sola. Vorrebbe visualizzarli in forma paginata sia sulla home che nel dettaglio della categoria e dei tag. Inoltre anche i tag e le categorie andranno paginate.    

Tommaso suggerisce di aggiungere la paginazione alla action *Index* del controller *HomeController* per permettere di visualizzare solo 3 posto alla volta. Verranno passati due parametri in querystring, uno per il numero di pagina, l'altro per indicare quanti elementi visualizzare in ogni pagina. Stessa cosa per le altre action che vanno paginate.  

### Specifiche implementative

#### Database
- Aggiungi altri post al database per far si che siano più di 3 e vedere la paginazione funzionare. Aggiungi per ogni nuovo post il valore della categorie e autore. Valorizza anche la tabella TagPosts di conseguenza.   

#### Backend

##### Progetto Domain
- Aggiungi una classe *IPagination.cs* nella cartella */Interfaces/Models*, dovrà avere le seguenti proprietà:
    - *PageNumber* di tipo *int*  
    - *PageSize* di tipo *int*  
- Aggiungi una classe *Pagination.cs* nella cartella */Models* che deve implementare l'interfaccia *IPagination* e aggiungi alle proprietà un valore di default 1 e 3 (rispettivamente per PageNumber e per PageSize)    
- Modifica l'interfaccia *IPostsRepository.cs* nella cartella */Interfaces/Repositories/* e crea un nuovo metodo come il *GetAll()*, ma che riceva come parametri due interi: il numero di pagina e quanti elementi per pagina:  
```csharp
public IEnumerable<Post> GetPaginatedAll(int page, int pageSize);
```
- Modifica l'interfaccia *IPostsService.cs* nella cartella */Interfaces/Services/* e crea un nuovo metodo come il *GetAll()*, ma che riceva come parametri due interi: il numero di pagina e quanti elementi per pagina:  
```csharp
public List<Post> GetPaginatedAll(int page, int pageSize);
```

##### Progetto UnitTest DAL (opzionale, ma vivamente consigliato)
- Aggiungi un nuovo metodo alla classe *PostsHelper* nella cartella */Helpers* per recuperare un numero di post sufficienti a testare la paginazione (ad esempio 4, se *pageSize* è 3), usa la funzione *GetDefaultMockData* come una traccia, copia e adatta il corpo del metodo.  
- Aggiungi un test nella classe *PostsRepositoryTest.cs* nella cartella */Repositories*, aggiungi un metodo di test *should_retrieve_all_paginated_posts*. Usa il metodo *should_retrieve_all_posts* come una traccia, copialo e adattalo per verificare il recupero dei post paginati.  
- Aggiungi altri test a piacere per verificare il recupero dei dati paginati utilizzando diversi parametri di ingresso (numero di pagina e quanti elementi per pagina)  

##### Progetto DAL
- Modifica la classe *PostsRepository.cs* nella cartella */Repositories* e crea un metodo per implementare quello dell'interfaccia *GetPaginatedAll* creato nel progetto *Domain*. Copia ed incolla il corpo del metodo *GetAll* e adatta la query per permettere di recuperare solo gli elementi richiesti dalla paginazione.  

###### Fai attenzione! In base al database che usi dovrai utilizzare una sintassi diversa per recuperare i valori paginati.
Se vuoi provare ad implementare il metodo per entrambi i database puoi usare il parametro di configurazione nell'appsettings che usiamo anche in *DatabaseConnectionFactory*. Per i test la sintassi da utilizzare per SQLite è la stessa di MySQL.  

MySQL
```sql
LIMIT @offset, @pageSize
```

Sql Server
```sql
OFFSET @offset ROWS FETCH NEXT @PageSize ROWS ONLY
```  

##### Progetto UnitTest BL (opzionale, ma vivamente consigliato)
- Aggiungi un nuovo metodo alla classe *PostsHelper* nella cartella */Helpers* per recuperare un numero di post sufficienti a testare la paginazione (ad esempio 4, se *pageSize* è 3), usa la funzione *GetDefaultMockData* come una traccia, copia e adatta il corpo del metodo.  
- Aggiungi un nuovo metodo di test *should_retrieve_all_paginated_posts* nella classe *PostsServiceTest.cs* che si trova nella cartella */Services*. Il metodo dovrà verificare il corretto recupero dei post paginati.  
- Aggiungi altri test a piacere per verificare il recupero dei dati paginati utilizzando diversi parametri di ingresso (numero di pagina e quanti elementi per pagina)  

##### Progetto BL
- Modifica la classe *PostsService.cs* nella cartella */Services* e crea un metodo per implementare quello dell'interfaccia *GetPaginatedAll* creato nel progetto Domain. Copia ed incolla il corpo del metodo *GetAll* e modificalo per permettere di chiamare il giusto metodo del repository.  


##### Progetto Web  
- Modifica la action *Index* nel controller *HomeController* per permettere il recupero dei parametri in querystring *page* and *pageSize* entrambi nullabili e con valore di default (1 e 3 rispettivamente).  
```csharp
public IActionResult Index(int page = 1, int pageSize = 3, string author = null)
```
inoltre prima del comando *return View(posts);* utilizzeremo il *ViewBag* per passare dei parametri alla View:   
```csharp
ViewBag.CurrentPage = page;
ViewBag.PageSize = pageSize;
ViewBag.IsFirst = ((int)ViewBag.CurrentPage > 1);
ViewBag.IsLast = (posts.Count >= (int)ViewBag.PageSize);
```

- Crea una *Partial View* nella cartella *Views/Shared* chiamata *_PaginationPartial.cshtml' e inserisci questi codici al suo interno  
```razor
@model string
@{ 
    var actionPath = (string)ViewBag.ActionPath;
    if(String.IsNullOrEmpty(actionPath))
    {
        actionPath = "Index";
    }
}
<div class="post-navigation">
    @if (ViewBag.IsFirst)
    {
        <a href="@Url.Action(actionPath, Model, new { page = (ViewBag.CurrentPage - 1), pageSize = ViewBag.PageSize })">Prev</a>
    }
    @if (ViewBag.IsFirst && ViewBag.IsLast)
    {
        <span> | </span>
    }
    @if (ViewBag.IsLast)
    {
        <a href="@Url.Action(actionPath, Model, new { page = (ViewBag.CurrentPage + 1), pageSize = ViewBag.PageSize })">Next</a>
    }
</div>
```
- Modifica la View *Index* nella cartella *Views/Home* e includi la Partial creata tramite questo comando (il parametro *ActionPath* in questo caso è opzionale e può essere omesso perché la Partial di default setta il valore ad *Index*, ma è utile per riutilizzare la partial in altre situazioni)  
```razor
@await Html.PartialAsync("_PaginationPartial", "Home" , new ViewDataDictionary(ViewData) { { "ActionPath", "Index" } })
```

#### Modifica le entità Categoria e Tag (opzionale, ma vivamente consigliato)
- Effettua le stesse modifiche che abbiamo fatto per i Post per le Categorie ed i Tag, così che anche questi saranno visualizzati paginati.  


[Vedi il repository con l'implementazione (!!!contiene spoiler)](https://github.com/Magicianred/my-blog-sample/tree/pathFromV1toV2/step04/add-pagination-to-posts)  


[Ritorna alla pagina principale](../README_IT.md)  
