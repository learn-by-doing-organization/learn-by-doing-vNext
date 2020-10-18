# My Blog Sample  

## Aggiungere le categorie ai Post [database, backend, frontend]
Giacomo vuole creare delle categorie logiche per raccogliere i Post, vorrebbe che i Post siano collegati ad una categoria, per ora non gli importa di poterli collegare a più di una categoria, ne basta una sola.  

Tommaso suggerisce di inserire una nuova tabella per le categorie e di aggiungere nella tabella dei Post un riferimento alla categoria.  

### Specifiche implementative  

#### Database
- Crea una tabella chiamata *Categories* con le seguenti colonne:  
    - *Id* [int, chiave primaria],  
    - *Name* [stringa],  
    - *Description* [stringa],  
    - *CreateDate* [datetime])  
- Crea nuova colonna nella tabella *Posts* chiamata *CategoryId*, che sarà chiave esterna sull'id della tabella delle categorie.  

#### Backend  

##### Progetto Domain  
- Aggiungi un'interfaccia *ICategory.cs* nella cartella */Interfaces/Models*, usa la *IPost.cs* come riferimento  
- Aggiungi un'interfaccia *ICategoriesRepository.cs* nella cartella */Interfaces/Repositories*, usa la *IPostsRepository.cs* come riferimento  
- Aggiungi un'interfaccia *ICategoriesService.cs* nella cartella */Interfaces/Services*, usa la *IPostsService.cs* come riferimento  
- Aggiungere una classe *Category.cs* nella cartella */Models*, usa la *Post.cs* come riferimento, ma aggiungi una proprietà per tenere i post della categoria:  
```csharp
public List<Post> Posts { get; set; }
```  

##### Progetto UnitTest DAL (opzionale, ma vivamente consigliato)  
- Aggiungi una classe *Category.cs* nella cartella */Models*, usa la classe *Post.cs* come riferimento
- Aggiungi una classe *CategoriesHelper.cs* nella cartella */Helpers*, usa la classe *PostsHelper.cs* come riferimento  
- Aggiungi una classe *CategoriesRepositoryTest.cs* nella cartella */Repositories*, usa la classe *PostsRepositoryTest.cs* come riferimento  

###### Fai attenzione, nella classe *CategoriesRepositoryTest.cs* usa la class *Category* che hai creato in questo progetto, non quella del progetto *Domain*. Questa è un'eccezione dovuta al fatto che il database InMemory non riconosce correttamente il nome della tabella, con questo *hack* tu puoi passare il nome della tabella attraverso l'attributo della classe *Post*, o nella tua implementazione *Categoria* (Tommaso sta ancora lavorando per risolvere correttamente questa casistica).  
```csharp
[Alias("Posts")]
```

##### Progetto DAL  
- Aggiungi la classe *CategoriesRepository.cs* nella cartella */Repositories*, usa la classe *PostsRepository.cs* come riferimento  

##### Progetto UnitTest BL (opzionale, ma vivamente consigliato)  
- Aggiungi la classe *CategoriesHelper.cs* nella cartella */Helpers*, usa la classe *PostsHelper.cs* come riferimento  
- Aggiungi la classe *CategoriesServiceTest.cs* nella cartella */Services*, usa la classe *PostsServiceTest.cs* come riferimento  

##### Progetto BL  
- Aggiungi la classe *CategoriesService.cs* nella cartella */Services*, usa la classe *PostsService.cs* come riferimento, tieni però presente che dovrai recuperare oltre i dati della categoria richiesta anche quelli dei post contenuti  
```csharp
category.Posts = connection.Query<Post>("SELECT Id, Title, Text FROM Posts WHERE CategoryId = @id ORDER BY CreateDate DESC", id);
```

#### Progetto Web  
- Aggiungi la action *Categories* nel controller *HomeController*, usa la action *Index* come riferimento  
- Aggiungi la action *Category({id})* nel controller *HomeController*, usa la action *Post({id})* come riferimento  
- Aggiungi la view *Categories* nella cartella *Views/Home*, usa la view *Index* come un riferimento  
- Aggiungi la view *Category* nella cartella *Views/Home*, usa la view *Post* come un riferimento, ma ricorda che dovrai visualizzare anche la lista dei post contenuti nella categoria, per questo vedi il *foreach* nella view *Index*  

