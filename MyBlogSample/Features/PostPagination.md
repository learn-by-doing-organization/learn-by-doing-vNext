# My Blog Sample
([Italian translate](PostPagination_IT.md))  

### Add pagination to the Post list [backend, frontend]
Jim already knows that the blog will soon fill up with posts and he does not want that all of posts to be visible on the home page at once. He would like to view them in paginated form both on the home page and in detail of the category and tags. In addition, also the tags and categories will be paginated.

Tom suggests adding pagination to the *Index* action of the *HomeController* controller to allow to be displayed only 3 posts at a time. Two parameters will be passed in the querystring, one for the page number, and the other to indicate how many items can display on each page. Same thing for the other actions that must be paginated.

### Implementation specifications

#### Database
- Add the other posts to database to makes it to be more than 3 posts and see to work pagination correctly. Add the value's of category and author for each new post. Verify also the TagPosts table Consequently.

#### Backend

##### Domain Project
- Add the *IPagination.cs* class to the */Interfaces/Models* folder. It must have the following properties:
    - *PageNumber* of type *int*  
    - *PageSize* of type *int*
- Add the *Pagination.cs* class to */Models* folder which must implement the interface *IPagination* and add to the properties the default value of 1 and 3 (for PageNumber and PageSize respectively)
- Modify the interface *IPostsRepository.cs* in the folder */Interfaces/Repositories/* and create a new method such as *GetAll()* which receives two integers as parameters: the page number and how many elements for page:
```csharp
public IEnumerable<Post> GetPaginatedAll(int page, int pageSize);
```
##### UnitTest DAL Project (optional, but highly recommended)
-Add a new method to *PostsHelper* class in the */Helpers* folder to retrieve enough posts to test the pagination (for example 4, if *pageSize* is 3), use the function *GetDefaultMockData* as a trace, copy and adapts the body of the method.
- Add a test to *PostsRepositoryTest.cs* class in the */Repositories* folder, add a tset method named *should_retrieve_all_paginated_posts*. use the method *should_retrieve_all_posts* as a trace, copy and adapts it to verify the retrieve of paginated posts. 
- Add other tests as desired to verify the retrieve of paginated data using different input parameters (page number and how many elements for page)

##### DAL Project
- Modify the *PostsRepository.cs* class in the */Repositories* folder and create a method to implement the *GetPaginatedAll* interface created in the project *Domain*. Copy and paste the body of the *GetAll* method and adapt the query which allow you to retrieve only the elements required by pagination.

###### Be careful! depending on which database you are using, you have to use a different syntax to retrieve the paginated values.
If you want to implement the method for both databases, can use the configuration parameter in the appsettings which we also use in *DatabaseConnectionFactory*. For the tests the syntax to be used for SQLite is the same as the MySQL.

MySQL
```sql
LIMIT @offset, @pageSize
```
Sql Server
```sql
OFFSET @offset ROWS FETCH NEXT @PageSize ROWS ONLY
``` 
##### UnitTest BL Project (optional, but highly recommended) 
- Add a new method to *PostsHelper* class in the folder */Helper* to retrieve enough posts to test pagination (for example 4, if *pageSize* is 3), use the function *GetDefaultMockData* as a trace, copy and adapts the body of the method.
- Add a new test method *should_retrieve_all_paginated_posts* in the *PostsServiceTest.cs* class in the folder */Services*. this method will have to verify the correct retrieve of paginated posts.
- Add other tests as desired to verify the retrieve of paginated data using different input parameters (the page number and how many elements for page)

##### BL Project
- Modify *PostsService.cs* class in the folder */Services* and create a method for implementing *GetPaginatedAll* of the interface created in the Domain project. Copy and paste the body of the *GetAll* method and modify it to allow you to call the correct repository method.

##### Web Project
- Modify the action *Index* in *HomeController* to allow the retrieve of the parameters in querystring *page* and *pageSize* both nullable and with default value (1 and 3 respectively).
```csharp
public IActionResult Index(int page = 1, int pageSize = 3, string author = null)
```
Moreover, before the *return View (posts);* command we will use the *ViewBag* to pass parameters to the View:
```csharp
ViewBag.CurrentPage = page;
ViewBag.PageSize = pageSize;
ViewBag.IsFirst = ((int)ViewBag.CurrentPage > 1);
ViewBag.IsLast = (posts.Count >= (int)ViewBag.PageSize);
```
- Create a *Partial View* in the *Views/Shared* folder called *_PaginationPartial.cshtml* and put these codes inside that:
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
- Modify the View *Index* in the folder *Views/Home* and include the Partial created via this command (the *ActionPath* parameter in this case is optional and can be omitted because the default Partial sets the value to Index, but it is useful for reusing the partial in other situations)
```razor
@await Html.PartialAsync("_PaginationPartial", "Home" , new ViewDataDictionary(ViewData) { { "ActionPath", "Index" } })
```

#### Modify Categoria e Tag entity (optional, but highly recommended)
- Make the same changes that we did for the Posts, for Categories and Tags, in the way that these two also will be displayed paginated.

[see the repository with the implementation (!!!contains spoiler)](https://github.com/Magicianred/my-blog-sample/tree/pathFromV1toV2/step04/add-pagination-to-posts) 

[Return to main page](../README.md)  
