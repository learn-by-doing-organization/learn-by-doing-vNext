# My Blog Sample  
([English translate](PostTags.md))  

## Aggiungere i tag ai Post [database, backend, frontend]
Giacomo ha saputo da un amico che lavora nel SEO che i tag sono molto comodi, quindi vuole aggiungerli anche lui al suo blog.
Tommaso suggerisce di creare una nuova tabella per i Tag e di creare una tabella di relazione con i Post

### Specifiche implementative   
#### Database
- Crea una tabella chiamata *Tags* con le seguenti colonne:  
    - *Id* [int, chiave primaria],  
    - *Name* [stringa],  
    - *Description* [stringa],  
    - *CreateDate* [datetime])  
- Crea nuova colonna nella tabella *Posts* chiamata *CategoryId*, che sarà chiave esterna sull'id della tabella delle categorie  
    - *CategoryId* [int]  

#### Backend  

##### Progetto Domain  
- Aggiungi un'interfaccia *ITag.cs* nella cartella */Interfaces/Models*, usa la *IPost.cs* come riferimento  
- Aggiungi un'interfaccia *ITagsRepository.cs* nella cartella */Interfaces/Repositories*, usa la *IPostsRepository.cs* come riferimento  
- Aggiungi un'interfaccia *ITagsService.cs* nella cartella */Interfaces/Services*, usa la *IPostsService.cs* come riferimento  
- Aggiungere una classe *Tag.cs* nella cartella */Models*, usa la *Post.cs* come riferimento  

[TO COMPLETE]  

##### Progetto UnitTest DAL (opzionale, ma vivamente consigliato)  
- Aggiungi una classe *Tag.cs* nella cartella */Models*, usa la classe *Post.cs* come riferimento
- Aggiungi una classe *TagsHelper.cs* nella cartella */Helpers*, usa la classe *PostsHelper.cs* come riferimento  
- Aggiungi una classe *TagsRepositoryTest.cs* nella cartella */Repositories*, usa la classe *PostsRepositoryTest.cs* come riferimento  

###### Fai attenzione, nella classe *CategoriesRepositoryTest.cs* usa la class *Category* che hai creato in questo progetto, non quella del progetto *Domain*. Questa è un'eccezione dovuta al fatto che il database InMemory non riconosce correttamente il nome della tabella, con questo *hack* tu puoi passare il nome della tabella attraverso l'attributo della classe *Post*, o nella tua implementazione *Categoria* (Tommaso sta ancora lavorando per risolvere correttamente questa casistica).  
```csharp
[Alias("Posts")]
```

##### Progetto DAL  
- Aggiungi la classe *TagsRepository.cs* nella cartella */Repositories*, usa la classe *PostsRepository.cs* come riferimento  

##### Progetto UnitTest BL (opzionale, ma vivamente consigliato)  
- Aggiungi la classe *TagsHelper.cs* nella cartella */Helpers*, usa la classe *PostsHelper.cs* come riferimento  
- Aggiungi la classe *TagsServiceTest.cs* nella cartella */Services*, usa la classe *PostsServiceTest.cs* come riferimento  

##### Progetto BL  
- Aggiungi la classe *TagsService.cs* nella cartella */Services*, usa la classe *PostsService.cs* come riferimento, tieni però presente che dovrai recuperare oltre i dati della categoria richiesta anche quelli dei post contenuti  
```csharp
category.Posts = connection.Query<Post>("SELECT Id, Title, Text FROM Posts WHERE CategoryId = @id ORDER BY CreateDate DESC", id);
```

[TO COMPLETE]

#### Progetto Web  
- Aggiungi la action *Tags* nel controller *HomeController*, usa la action *Index* come riferimento  
- Aggiungi la action *Tag({id})* nel controller *HomeController*, usa la action *Post({id})* come riferimento  
- Aggiungi la view *Tags* nella cartella *Views/Home*, usa la view *Index* come come una traccia, copia il codice e adattalo  
- Aggiungi la view *Tag* nella cartella *Views/Home*, usa la view *Post* come come una traccia, copia il codice e adattalo, ma ricorda che dovrai visualizzare anche la lista dei post contenuti nel tag, per questo vedi il *foreach* nella view *Index*  

[Ritorna alla pagina principale](../README_IT.md)  