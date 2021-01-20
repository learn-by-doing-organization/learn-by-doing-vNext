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
     - * CreateDate * [datetime]  
- Create new column in *Posts* table named *CategoryId*, which will be foreign key on category table id.  

#### Backend

##### Domain Project
- Add an *ICategory.cs* interface in the */Interfaces/Models* folder, use the *IPost.cs* as a trace, copy the code and adapt it, but add a property to hold the category posts:  
```csharp
public List<Post> Posts { get; set; }
```  
- Add an *ICategoriesRepository.cs* interface in the */Interfaces/Repositories* folder, use the *IPostsRepository.cs* as a trace, copy the code and adapt it  
- Add an *ICategoriesService.cs* interface in the */Interfaces/Services* folder, use the *IPostsService.cs* as a trace, copy the code and adapt it  
- Add a *Category.cs* class in the */Models* folder, use the *Post.cs* as a trace, copy the code and adapt it  
- Add a property *CategoryId* in interface */Interfaces/Models/IPost.cs* and in class */Models/Post.cs*  

##### UnitTest DAL project (optional, but highly recommended)
- Add a *Category.cs* class in the */Models* folder, use the *Post.cs* class as a trace, copy the code and adapt it  
- Add a *CategoriesHelper.cs* class in the */Helpers* folder, use the *PostsHelper.cs* class as a trace, copy the code and adapt it  
- Add a *CategoriesRepositoryTest.cs* class in the */Repositories* folder, use the *PostsRepositoryTest.cs* class as a trace, copy the code and adapt it. (In the test that verifies the retrieve of a category you will also have to insert the posts in the InMemory database, otherwise you will receive an error).  
```csharp
// insert post because of InMemory DB must have table Posts
var mockPosts = PostsHelper.GetDefaultMockData();
db.Insert<Post>(mockPosts);
```  

###### Be careful, in the *CategoriesRepositoryTest.cs* class use the *Category* class you created in this project, not the *Domain* project one. This is an exception due to the InMemory database not recognizing the table name correctly, with this *hack* you can pass the table name through the *Post* class attribute, or in your implementation *Category* (Tom is still working to solve this case correctly).
```csharp
[Alias("Posts")]
```

###### Be careful, the test project doesn't compile because of there are no class in DAL Project. It's ok, in TDD practice you write before the test and then you write code for use it.

##### DAL Project
 Add *CategoriesRepository.cs* class in */Repositories* folder, use *PostsRepository.cs* class as trace, copy the code and adapt it, but remember to retrieve all posts of the category in the property:  
```csharp
public List<Post> Posts { get; set; }
```   

##### Progetto UnitTest BL (opzionale, ma vivamente consigliato)
- Add *CategoriesHelper.cs* class in */Helpers* folder, use *PostsHelper.cs* class as trace, copy the code and adapt it  
- Add *CategoriesServiceTest.cs* class in */Services* folder, use *PostsServiceTest.cs* class as trace, copy the code and adapt it  

##### BL Project
- Add the *CategoriesService.cs* class in the */Services* folder, use the *PostsService.cs* class as a trace, copy the code and adapt it  

####  Web Project
- Add the *Categories* action in the *HomeController* controller, use the *Index* action as a trace, copy the code and adapt it  
- Add the *Category({id})* action in the *HomeController* controller, use the *Post({id})* action as a trace, copy the code and adapt it  
- Add the *Categories* view in the *Views/Home* folder, use the *Index* view as a trace, copy the code and adapt it  
- Add the *Category* view in the *Views/Home* folder, use the *Post* view as a trace, copy the code and adapt it, but remember that you will also have to display the list of posts contained in the category, for this you see the *foreach* in the *Index view*  
- Add a link to Categories page in *Views/Shared/_Layout.cshtml*, you can copy and past the link Home and adapt it  
```razor
<a href="@Url.Action("Categories", "Home")" data-rb-event-key="about" class="nav-link">Categories</a>
```  
- In file *Startup.cs* add code to handle dependence injection for the new interfaces and classes, inside the function *ConfigureServices*:  
```csharp
services.AddScoped<ICategory, Category>();
services.AddScoped<ICategoriesRepository, CategoriesRepository>();
services.AddScoped<ICategoriesService, CategoriesService>();
```  

#### Integration Test Web Project
- Add a test like *HomeControllerTest.should_retrieve_all_posts* to verify that the categories page responds correctly  
- Add a test like *HomeControllerTest.should_retrieve_post_by_id* to verify that the category page responds correctly when requesting an existing id  
- Add a test like *HomeControllerTest.should_retrieve_no_one_post* to verify that the category page responds correctly when requesting a non-existent id  

[See the repository with the implementation (!!! contains spoilers)](https://github.com/Magicianred/my-blog-sample/tree/pathFromV1toV2/step01/add-category-to-posts)  

[Return to main page](../README.md)  