# My Blog Sample  
([Italian translate](PostCategories_IT.md))  

### Add categories to Posts [database, backend, frontend]  
Jim wants to create logical categories to collect the Posts. He would like the Posts to be linked to a category, for now he doesn't mind being able to link them to more than one category, only one is enough.  

Tom suggests inserting a new table for the categories and adding a reference to the category in the Post table.  

### Implementation specifications  

#### Database  
- Create a table called *Categories* with the following columns:  
     - * Id * [int, primary key],  
     - * Name * [string],  
     - * Description * [string],  
     - * CreateDate * [datetime])  
- Create new column in *Posts* table named *CategoryId*, which will be foreign key on category table id.  

#### Backend  

##### Domain Project  
- Aggiungi un'interfaccia *ICategory.cs* nella cartella */Interfaces/Models*, usa la *IPost.cs* come riferimento  
- Aggiungi un'interfaccia *ICategoriesRepository.cs* nella cartella */Interfaces/Repositories*, usa la *IPostsRepository.cs* come riferimento  
- Aggiungi un'interfaccia *ICategoriesService.cs* nella cartella */Interfaces/Services*, usa la *IPostsService.cs* come riferimento  
- Aggiungere una classe *Category.cs* nella cartella */Models*, usa la *Post.cs* come riferimento, ma aggiungi una proprietà per tenere i post della categoria:  
- Add an *ICategory.cs* interface in the */Interfaces/Models* folder, use the *IPost.cs* as a reference  
- Add an *ICategoriesRepository.cs* interface in the */Interfaces/Repositories* folder, use the *IPostsRepository.cs* as a reference  
- Add an *ICategoriesService.cs* interface in the */Interfaces/Services* folder, use the *IPostsService.cs* as a reference  
- Add a *Category.cs* class in the */Models* folder, use the *Post.cs* as a reference, but add a property to hold the category posts:  
```csharp
public List<Post> Posts { get; set; }
```  

##### UnitTest DAL project (optional, but highly recommended)  
- Add a *Category.cs* class in the */Models* folder, use the *Post.cs* class as a reference  
- Add a *CategoriesHelper.cs* class in the */Helpers* folder, use the *PostsHelper.cs* class as a reference  
- Add a *CategoriesRepositoryTest.cs* class in the */Repositories* folder, use the *PostsRepositoryTest.cs* class as a reference  

###### Be careful, in the *CategoriesRepositoryTest.cs* class use the *Category* class you created in this project, not the *Domain* project one. This is an exception due to the InMemory database not recognizing the table name correctly, with this *hack* you can pass the table name through the *Post* class attribute, or in your implementation *Category* (Tom is still working to solve this case correctly).  
```csharp
[Alias("Posts")]
```

##### DAL Project  
 Add *CategoriesRepository.cs* class in */Repositories* folder, use *PostsRepository.cs* class as reference  

##### Progetto UnitTest BL (opzionale, ma vivamente consigliato)  
- Add *CategoriesHelper.cs* class in */Helpers* folder, use *PostsHelper.cs* class as reference  
- Add *CategoriesServiceTest.cs* class in */Services* folder, use *PostsServiceTest.cs* class as reference  

##### BL Project  
- Aggiungi la classe *CategoriesService.cs* nella cartella */Services*, usa la classe *PostsService.cs* come riferimento, tieni però presente che dovrai recuperare oltre i dati della categoria richiesta anche quelli dei post contenuti  
- Add the *CategoriesService.cs* class in the */Services* folder, use the *PostsService.cs* class as a reference, but keep in mind that you will have to retrieve the data of the requested category as well as those of the posts contained  
```csharp
category.Posts = connection.Query<Post>("SELECT Id, Title, Text FROM Posts WHERE CategoryId = @id ORDER BY CreateDate DESC", id);
```

####  Web Project  
- Add the *Categories* action in the *HomeController* controller, use the *Index* action as a reference  
- Add the *Category({id})* action in the *HomeController* controller, use the *Post({id})* action as a reference  
- Add the *Categories* view in the *Views/Home* folder, use the *Index* view as a reference  
- Add the *Category* view in the *Views/Home* folder, use the *Post* view as a reference, but remember that you will also have to display the list of posts contained in the category, for this you see the *foreach* in the *Index view*  

[Return to main page](../README.md)  