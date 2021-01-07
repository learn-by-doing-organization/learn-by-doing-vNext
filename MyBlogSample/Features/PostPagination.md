# My Blog Sample
([Italian translate](PostPagination_IT.md))  

### Add pagination to the Post list [backend, frontend]
Jim already knows that the blog will soon fill up with posts and he does not want that all of posts to be visible on the home page at once. He would like to view them in paginated form both on the home page and in detail of the category and tags. In addition, also the tags and categories will be paginated.

Tomas suggests adding pagination to the *Index* action of the *HomeController* controller to allow to be displayed only 3 posts at a time. Two parameters will be passed in the querystring, one for the page number, and the other to indicate how many items can display on each page. Same thing for the other actions that must be paginated.

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
##### UnitTest DAL (optional, but highly recommended)
-Add a new method to *PostsHelper* class in the */Helpers* folder to retrieve enough posts to test the pagination (for example 4, if *pageSize* is 3), use the function *GetDefaultMockData* as a trace, copy and adapts the body of the method.
- Add a test to *PostsRepositoryTest.cs* class in the */Repositories* folder, add a tset method named *should_retrieve_all_paginated_posts*. use the method *should_retrieve_all_posts* as a trace, copy and adapts it to verify the recovery of paginated posts. 
- Add other tests as desired to verify the recovery of paginated data using different input parameters (page number and how many elements for page)

##### Progetto DAL
- Modify the *PostsRepository.cs* class in the */Repositories* folder and create a method to implement the *GetPaginatedAll* interface created in the project *Domain*. Copy and paste the body of the *GetAll* method and adapt the query which allow you to retrieve only the elements required by pagination.

###### Be careful! depending on which database you are using, you have to use a different syntax to retrieve the paginated values.
If you want to implement the method for both databases you can use the configuration parameter in the appsettings which we also use in *DatabaseConnectionFactory*. For the tests the syntax to be used for SQLite is the same as the MySQL.

MySQL
```sql
LIMIT @offset, @pageSize
```
Sql Server
```sql
OFFSET @offset ROWS FETCH NEXT @PageSize ROWS ONLY
``` 


[TO DO]  

[Return to main page](../README.md)  
