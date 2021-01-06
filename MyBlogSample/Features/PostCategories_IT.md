# My Blog Sample - Specifiche implementative
([English translate](PostCategories.md))  

## Aggiungere le categorie ai Post [database, backend, frontend]
Giacomo vuole creare delle categorie logiche per raccogliere i Post, vorrebbe che i Post siano collegati ad una categoria, per ora non gli importa di poterli collegare a più di una categoria, ne basta una sola.  

Tommaso suggerisce di inserire una nuova tabella per le categorie e di aggiungere nella tabella dei Post un riferimento alla categoria.  

### Specifiche implementative

#### Database
- Crea una tabella chiamata *Categories* con le seguenti colonne:  
    - *Id* [int, chiave primaria],  
    - *Name* [stringa],  
    - *Description* [stringa],  
    - *CreateDate* [datetime]  
- Crea nuova colonna nella tabella *Posts* chiamata *CategoryId*, che sarà chiave esterna sull'id della tabella delle categorie.  

#### Backend

##### Progetto Domain
- Aggiungi un'interfaccia *ICategory.cs* nella cartella */Interfaces/Models*, usa la *IPost.cs* come una traccia, copia il codice e adattalo, ma aggiungi una proprietà per tenere i post della categoria:  
```csharp
public List<Post> Posts { get; set; }
```  
- Aggiungi un'interfaccia *ICategoriesRepository.cs* nella cartella */Interfaces/Repositories*, usa la *IPostsRepository.cs* come una traccia, copia il codice e adattalo  
- Aggiungi un'interfaccia *ICategoriesService.cs* nella cartella */Interfaces/Services*, usa la *IPostsService.cs* come una traccia, copia il codice e adattalo  
- Aggiungere una classe *Category.cs* nella cartella */Models*, usa la *Post.cs* come una traccia, copia il codice e adattalo  
- Aggiungi la proprietà *CategoryId* nell'interfaccia */Interfaces/Models/IPost.cs* e nella classe */Models/Post.cs*  

##### Progetto UnitTest DAL (opzionale, ma vivamente consigliato)
- Aggiungi una classe *Category.cs* nella cartella */Models*, usa la classe *Post.cs* come una traccia, copia il codice e adattalo
- Aggiungi una classe *CategoriesHelper.cs* nella cartella */Helpers*, usa la classe *PostsHelper.cs* come una traccia, copia il codice e adattalo  
- Aggiungi una classe *CategoriesRepositoryTest.cs* nella cartella */Repositories*, usa la classe *PostsRepositoryTest.cs* come una traccia, copia il codice e adattalo. (Nel test che verifica il recupero di una categoria dovrai inserire nel database InMemory anche i post, altrimenti riceverai un errore).  
```csharp
// insert post because of InMemory DB must have table Posts
var mockPosts = PostsHelper.GetDefaultMockData();
db.Insert<Post>(mockPosts);
```  

###### Fai attenzione, nella classe *CategoriesRepositoryTest.cs* usa la classe *Category* che hai creato in questo progetto, non quella del progetto *Domain*. Questa è un'eccezione dovuta al fatto che il database InMemory non riconosce correttamente il nome della tabella, con questo *hack* tu puoi passare il nome della tabella attraverso l'attributo della classe *Category*, o nella tua implementazione *Category* (Tommaso sta ancora lavorando per risolvere correttamente questa casistica).
```csharp
[Alias("Posts")]
```

###### Fai attenzione, il progetto di test non compila perché non ci sono le classi nel progetto DAL. E' giusto, nella pratica TDD tu scrivi prima il test e poi scrivi il codice per usarlo.

##### Progetto DAL
- Aggiungi la classe *CategoriesRepository.cs* nella cartella */Repositories*, usa la classe *PostsRepository.cs* come una traccia, copia il codice e adattalo, ma ricordati di recuperare tutti i post della categoria nella proprietà:  
```csharp
public List<Post> Posts { get; set; }
```   

##### Progetto UnitTest BL (opzionale, ma vivamente consigliato)
- Aggiungi la classe *CategoriesHelper.cs* nella cartella */Helpers*, usa la classe *PostsHelper.cs* come una traccia, copia il codice e adattalo  
- Aggiungi la classe *CategoriesServiceTest.cs* nella cartella */Services*, usa la classe *PostsServiceTest.cs* come una traccia, copia il codice e adattalo  

##### Progetto BL
- Aggiungi la classe *CategoriesService.cs* nella cartella */Services*, usa la classe *PostsService.cs* come una traccia, copia il codice e adattalo  

#### Progetto Web
- Aggiungi la action *Categories* nel controller *HomeController*, usa la action *Index* come una traccia, copia il codice e adattalo  
- Aggiungi la action *Category({id})* nel controller *HomeController*, usa la action *Post({id})* come una traccia, copia il codice e adattalo  
- Aggiungi la view *Categories* nella cartella *Views/Home*, usa la view *Index* come una traccia, copia il codice e adattalo  
- Aggiungi la view *Category* nella cartella *Views/Home*, usa la view *Post* come una traccia, copia il codice e adattalo, ma ricorda che dovrai visualizzare anche la lista dei post contenuti nella categoria, per questo vedi il *foreach* nella view *Index*  
- Aggiungi un link alla pagina delle Categorie nel file *Views/Shared/_Layout.cshtml*, puoi copiare ed incollare il link alla Home e adattarlo    
```razor
<a href="@Url.Action("Categories", "Home")" data-rb-event-key="about" class="nav-link">Categories</a>
```  
- Nel file *Startup.cs* aggiungi il codice per gestire la dependence injection per le nuove interfacce e classi, all'interno della funzione *ConfigureServices*:  
```csharp
services.AddScoped<ICategory, Category>();
services.AddScoped<ICategoriesRepository, CategoriesRepository>();
services.AddScoped<ICategoriesService, CategoriesService>();
```  

#### Progetto Integration Test Web
- Aggiungi un test come *HomeControllerTest.should_retrieve_all_posts* per verificare che la pagina delle categorie risponda correttamente  
- Aggiungi un test come *HomeControllerTest.should_retrieve_post_by_id* per verificare che la pagina della categoria risponda correttamente quando si richiede un id esistente  
- Aggiungi un test come *HomeControllerTest.should_retrieve_no_one_post* per verificare che la pagina della categoria risponda correttamente quando si richiede un id non esistente  

[Vedi il repository con l'implementazione (!!!contiene spoiler)](https://github.com/Magicianred/my-blog-sample/tree/pathFromV1toV2/step01/add-category-to-posts)  

[Ritorna alla pagina principale](../README_IT.md)  

