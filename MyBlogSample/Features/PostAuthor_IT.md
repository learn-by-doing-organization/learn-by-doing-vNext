# My Blog Sample
([English translate](PostAuthor.md))  

## Aggiungere l'autore ai Post [database, backend, frontend]
Giacomo vorrebbe coinvoltere altri amici per redarre i post del blog, per questo ha bisogno di indicare nei post chi è l'autore. Al momento non pensa sia necessario creare l'entità Autori, basterà solo indicare l'autore.  
Inoltre avrebbe piacere che si possa avere una lista dei post di uno specifico autore.  

Tommaso suggerisce di aggiungere un campo Autore nella tabella dei Post e di passare un parametro in querystring per filtrare la lista dei post.  

### Specifiche implementative

#### Database
- Crea nuova colonna nella tabella *Posts* chiamata *Author*, che conterrà una stringa col nome dell'autore del post.  

#### Backend

##### Progetto Domain
- Aggiungi la proprietà *Author* nell'interfaccia */Interfaces/Models/IPost.cs* e, di conseguenza, nella classe */Models/Post.cs*  
- Modificare le interfaccie *IPostsRepository* nella cartella */Interfaces/Repositories* e *IPostsService* nella cartella */Interfaces/Services* aggiungendo in entrambe un nuovo metodo per filtrare la lista dei post  
```csharp
public IEnumerable<Post> GetAllByAuthor(string author);
```

##### Progetto UnitTest DAL (opzionale, ma vivamente consigliato)
- Modifica il metodo *GetDefaultMockData* della classe *PostsHelper* nella cartella */Helpers* aggiungendo la valorizzazione della nuova proprietà *Author*  
- Modifica il test *should_retrieve_all_posts* e *should_retrieve_post_by_id* aggiungendo un *Assert* che verifica la corretta valorizzazione della proprietà *Author*  
- Aggiungi un nuovo test per verificare la lista dei post filtrati per autore (*PostsRepository.GetAllByAuthor()*) dando in input al test parametri diversi (in base ai nomi degli autori che hai inserito nella *PostsHelper*) e verifica negli *Assert* che i post ritornati siano effettivamente di quell'autore  
```csharp
[TestCase("Tom")]
[TestCase("Jim")]
public void should_retrieve_all_posts_by_author(string author)
```
- Esegui i test della classe *PostsRepositoryTest* e verifica che ci sia un errore nell'asserzione che abbiamo aggiunto perché la proprietà *Author* dell'istanza tornata dalla chiamata è *null*  
- Riesegui i test dopo aver implementato le funzionalità nel progetto *DAL*  

##### Progetto DAL
- Modificare la classe *PostsRepository.cs* nella cartella */Repositories* aggiornando tutte le query presenti inserendo il recupero di *Author* nella *SELECT*  
```sql
SELECT Id, Title, Text, Author FROM Posts
```
- Modificare la classe *PostsRepository* nella cartella */Repositories* implementando il metodo dell'interfaccia facendo in modo che la query filtri per la proprietà *Author*    
```csharp
public IEnumerable<Post> GetAllByAuthor(string author);
```

##### Progetto UnitTest BL (opzionale, ma vivamente consigliato)
- Modifica il metodo *GetDefaultMockData* della classe *PostsHelper* nella cartella */Helpers* aggiungendo la valorizzazione della nuova proprietà *Author*  
- Aggiungi un nuovo test per verificare la lista dei post filtrati per autore (*PostsService.GetAllByAuthor()*) dando in input al test parametri diversi (in base ai nomi degli autori che hai inserito nella *PostsHelper*) e verifica negli *Assert* che i post ritornati siano effettivamente di quell'autore  
```csharp
[TestCase("Tom")]
[TestCase("Jim")]
public void should_retrieve_all_posts_by_author(string author)
```  

##### Progetto BL
- Modificare la classe *PostsService* nella cartella */Services* implementando il metodo dell'interfaccia facendo in modo che chiami il nuovo metodo del repository *GetAllByAuthor*    
```csharp
public IEnumerable<Post> GetAllByAuthor(string author);
```

#### Progetto Web
- Modificare la action *Index* nel controller *HomeController* facendo in modo che riceva un parametro *author* di tipo stringa
```csharp
public IActionResult Index(string author = null)
```
 e se valorizzato richiami il nuovo metodo *GetAllByAuthor* del service invece di *GetAll*  
```csharp
if (!String.IsNullOrWhiteSpace(author))
```

#### Progetto Integration Test Web
Nessun intervento  

[Vedi il repository con l'implementazione (!!!contiene spoiler)](https://github.com/Magicianred/my-blog-sample/tree/pathFromV1toV2/step03/add-author-to-posts)  

[Ritorna alla pagina principale](../README_IT.md)  
