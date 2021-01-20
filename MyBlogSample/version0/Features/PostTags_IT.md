# My Blog Sample
([English translate](PostTags.md))  

## Aggiungere i tag ai Post [database, backend, frontend]
Giacomo ha saputo da un amico che lavora nel SEO che i tag sono molto comodi, quindi vuole aggiungerli anche lui al suo blog.  

Tommaso suggerisce di creare una nuova tabella per i Tag e di creare una tabella di relazione con i Post.  

### Specifiche implementative

#### Database
- Crea una tabella chiamata *Tags* con le seguenti colonne:  
    - *Id* [int, chiave primaria],  
    - *Name* [stringa],  
    - *Description* [stringa],  
    - *CreateDate* [datetime]  
- Crea una tabella chiamata *PostTags* con le seguenti colonne:  
    - *PostId* [int, chiave primaria],  
    - *TagId* [int, chiave primaria]  

#### Backend

##### Progetto Domain
- Aggiungi un'interfaccia *ITag.cs* nella cartella */Interfaces/Models*, usa la *IPost.cs* come una traccia, copia il codice e adattalo, ma aggiungi una proprietà per tenere i post del tag:  
```csharp
public List<Post> Posts { get; set; }
```    
- Modifica l'interfaccia *IPost.cs* nella cartella */Inferfaces/Models* e aggiungi una proprietà per tenere dei tag del post:  
```csharp
public List<Tag> Tags { get; set; }
```    
- Aggiungi un'interfaccia *IPostTag.cs* nella cartella */Interfaces/Models*, usa la *IPost.cs* come una traccia, copia il codice e adattalo  
- Aggiungi un'interfaccia *ITagsRepository.cs* nella cartella */Interfaces/Repositories*, usa la *IPostsRepository.cs* come una traccia, copia il codice e adattalo  
- Aggiungi un'interfaccia *ITagsService.cs* nella cartella */Interfaces/Services*, usa la *IPostsService.cs* come una traccia, copia il codice e adattalo  
- Aggiungere una classe *Tag.cs* nella cartella */Models*, usa la *Post.cs* come una traccia, copia il codice e adattalo  
- Aggiungere una classe *PostTag.cs* nella cartella */Models*, usa la *Post.cs* come una traccia, copia il codice e adattalo  

##### Progetto UnitTest DAL (opzionale, ma vivamente consigliato)
- Aggiungi una classe *Tag.cs* nella cartella */Models*, usa la classe *Post.cs* come una traccia, copia il codice e adattalo  
- Aggiungi una classe *PostTag.cs* nella cartella */Models*, usa la classe *Post.cs* come una traccia, copia il codice e adattalo  
- Aggiungi una classe *PostTagsHelper.cs* nella cartella */Helpers*, usa la classe *PostsHelper.cs* come una traccia, copia il codice e adattalo  
- Modifica la classe *PostsHelper.cs* nella cartella */Helpers* aggiungendo il seguente metodo per valorizzare i post con i tag  
```csharp
public static List<Post> GetMockDataWithTags(List<Tag> mockTags)
{
    List<Post> mockPosts = PostsHelper.GetDefaultMockData();
    mockPosts[0].Tags = new List<Domain.Models.Tag>();
    mockPosts[0].Tags.Add(mockTags[0]);
    mockPosts[1].Tags = new List<Domain.Models.Tag>();
    mockPosts[1].Tags.Add(mockTags[1]);
    return mockPosts;
}
```  
- Aggiungi una classe *TagsHelper.cs* nella cartella */Helpers*, usa la classe *PostsHelper.cs* come una traccia, copia il codice e adattalo. Come per la PostsHelper.cs crea un metodo *GetMockDataWithPosts* per avere dei tag con i post.  
- Aggiungi un test nella classe *PostsRepositoryTest.cs* nella cartella */Repositories*, usa il test *should_retrieve_post_by_id* come una traccia, copialo e adattolo per verificare il recupero dei tag nel post.  
(per far funzionare il database InMemory devi inserire prima i Tag e i PostTag e poi i Post con all'interno i tag. Se non fai così riceverai un errore che nel database non c'è una tabella *Tags* o *PostTags*. Effettua questa correzione anche nel metodo *should_retrieve_all_posts*)  
```csharp
// Arrange
var mockTags = TagsHelper.GetDefaultMockData();
var mockPosts = PostsHelper.GetDefaultMockData();
var mockPostTags = PostTagsHelper.GetDefaultMockData();
var db = new InMemoryDatabase();
db.Insert<Tag>(mockTags);
db.Insert<Post>(mockPosts);
db.Insert<PostTag>(mockPostTags);
```
- Aggiungi una classe *TagsRepositoryTest.cs* nella cartella */Repositories*, usa la classe *PostsRepositoryTest.cs* come una traccia, copia il codice e adattalo  

###### Fai attenzione, nella classe *TagsRepositoryTest.cs* usa le classi *Tag* e *PostTag* che hai creato in questo progetto, non quelle del progetto *Domain*. Questa è un'eccezione dovuta al fatto che il database InMemory non riconosce correttamente il nome della tabella, con questo *hack* tu puoi passare il nome della tabella attraverso l'attributo della classe *Tag*, o nella tua implementazione *Tag* (Tommaso sta ancora lavorando per risolvere correttamente questa casistica).
```csharp
[Alias("Tags")]
```

###### Fai attenzione, il progetto di test non compila perché non ci sono le classi nel progetto DAL. E' giusto, nella pratica TDD tu scrivi prima il test e poi scrivi il codice per usarlo.

##### Progetto DAL
- Modifica la classe *PostsRepository.cs* nella cartella */Repositories* e recupera tutti i tag del post nella proprietà:  
```csharp
public List<Tag> Tags { get; set; }
```  
- Aggiungi la classe *TagsRepository.cs* nella cartella */Repositories*, usa la classe *PostsRepository.cs* come una traccia, copia il codice e adattalo, ma ricordati di recuperare tutti i post del tag nella proprietà:  
```csharp
public List<Post> Posts { get; set; }
```  

###### Fai attenzione, Dapper non è in grado di recupera le proprietà di tipo *List* per cui indica tutti i valori della *Projection* nella query, per esempio:
```sql
SELECT Id, Name, Description FROM Tags
```    

##### Progetto UnitTest BL (opzionale, ma vivamente consigliato)
- Aggiungi la classe *TagsHelper.cs* nella cartella */Helpers*, usa la classe *PostsHelper.cs* come una traccia  
- Aggiungi la classe *TagsServiceTest.cs* nella cartella */Services*, usa la classe *PostsServiceTest.cs* come una traccia, copia il codice e adattalo  
- Aggiungi altri test a piacere per verificare il recupero dei Tag del Post o dei Post del Tag

##### Progetto BL
- Aggiungi la classe *TagsService.cs* nella cartella */Services*, usa la classe *PostsService.cs* come una traccia, copia il codice e adattalo  

#### Progetto Web
- Aggiungi la action *Tags* nel controller *HomeController*, usa la action *Index* come una traccia, copia il codice e adattalo  
- Aggiungi la action *Tag({id})* nel controller *HomeController*, usa la action *Post({id})* come una traccia, copia il codice e adattalo  
- Aggiungi la view *Tags* nella cartella *Views/Home*, usa la view *Index* come come una traccia, copia il codice e adattalo  
- Aggiungi la view *Tag* nella cartella *Views/Home*, usa la view *Post* come come una traccia, copia il codice e adattalo, ma ricorda che dovrai visualizzare anche la lista dei post contenuti nel tag, per questo vedi il *foreach* nella view *Index*  
- Aggiungi un link alla pagina delle Categorie nel file *Views/Shared/_Layout.cshtml*, puoi copiare ed incollare il link alla Home e adattarlo    
```razor
<a href="@Url.Action("Tags", "Home")" data-rb-event-key="about" class="nav-link">Tags</a>
```  
- Nel file *Startup.cs* aggiungi il codice per gestire la dependence injection per le nuove interfacce e classi, all'interno della funzione *ConfigureServices*:  
```csharp
services.AddScoped<ITag, Tag>();
services.AddScoped<IPostTag, PostTag>();
services.AddScoped<ITagsRepository, TagsRepository>();
services.AddScoped<ITagsService, TagsService>();
```  

#### Progetto Integration Test Web
- Aggiungi un test come *HomeControllerTest.should_retrieve_all_posts* per verificare che la pagina dei tag risponda correttamente  
- Aggiungi un test come *HomeControllerTest.should_retrieve_post_by_id* per verificare che la pagina di dettaglio del tag risponda correttamente quando si richiede un id esistente  
- Aggiungi un test come *HomeControllerTest.should_retrieve_no_one_post* per verificare che la pagina di dettaglio del tag risponda correttamente quando si richiede un id non esistente  

[Vedi il repository con l'implementazione (!!!contiene spoiler)](https://github.com/Magicianred/my-blog-sample/tree/pathFromV1toV2/step02/add-tags-to-posts)  

[Ritorna alla pagina principale](../README_IT.md)  

