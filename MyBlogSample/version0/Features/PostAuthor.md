# My Blog Sample
([Italian translate](PostAuthor_IT.md))  

### Adding the Author to Posts [database, backend, frontend]

Jim would like to involve other friends to write posts of blog, so he needs to indicate in the posts who is the author. At the moment he think it not is necessary to create the Authors entity, it will be enough to indicate the author as string.
Also he would like to have a list of posts from a specific author.

Tom suggests inserting an Author field in the Posts table and pass a parameter in querystring to filter the list of post.

### Implementation specifications

#### Database

Create a new column in the Posts table called Author, which will contain a string with the name of the author's of post.

#### Backend

##### Domain Project

- Add the property *Author* in the *IPost.cs* interface in */Interfaces/Models/Ipost.cs*, and consequently for the */Models/Post.cs* class.
- Modify the *IPostsRepository* interface in the */Interfaces/Repositories* folder and *IPostsService* in the */Interfaces/Services* folder adding to the both of them a new method to filter the list of post:

```csharp
public IEnumerable<Post> GetAllByAuthor(string author);
```

##### UnitTest DAL project (optional, but highly recommended)

- Modify the method *GetDefaultMockData* in the *PostsHelper* class in */Helpers* folder adding a value into the new property.
- Modify the *should_retrieve_all_posts e should_retrieve_post_by_id* test by adding an *Assert* which verifies the correct value of the Author property.
- Add a new test to verify the list of post filtered by author (*PostsRepository.GetAllByAuthor()*) giving different input parameters to the test (based on the names of the authors which you have inserted in the PostsHelper) and verify in the *Asserts* that the returned posts are actually from that author.

```csharp
[TestCase("Tom")]
[TestCase("Jim")]
public void should_retrieve_all_posts_by_author(string author)
```
- Run the test of *PostsRepositoryTest* class and verify that there is an error in the assertion we added because the Author property of the instance returned from the call is null.
- Run again the test after implementing the functionality in the DAL project.

##### DAL Project

- Modify the *PostsRepository.cs* class in the */Repositories* folder updating all the present queries by inserting the recovery of Author in the SELECT

```csharp
SELECT Id, Title, Text, Author FROM Posts
```

- Modify the *PostsRepository.cs* class in the */Repositories* folder implementing the method of interface in the way that the query filtered by the Author property

```csharp
public IEnumerable<Post> GetAllByAuthor(string author);
```

##### UnitTest BL Project (optional, but highly recommended)

- Modify the *GetDefaultMockData* method of PostsHelper class in the */Helpers* folder adding a value to the the new Author property.
- Add a new test to verify the list of post filtered by author (*PostsService.GetAllByAuthor()*) giving different parameters as input to the test (based on the names of the authors you entered in the PostsHelper) and verify in the *Asserts* that the returned posts are actually of that author.

```csharp
[TestCase("Tom")]
[TestCase("Jim")]
public void should_retrieve_all_posts_by_author(string author)
```

##### BL Project

- Modify the class *PostsService* in the */Services* folder implementing the method of interface, in the way which call the new method of repository *GetAllByAuthor*

```csharp
public IEnumerable<Post> GetAllByAuthor(string author);
```

####  Web Project

- Modify the *Index* action in *HomeController* in the way which recieve a parameter (author) of string-type.

```csharp
public IActionResult Index(string author = null)
```
and if valued, call the new GetAllByAuthor method of the service instead of GetAll:

```csharp
if (!String.IsNullOrWhiteSpace(author))
```

#### Integration Test Web Project

No intervention

[See the repository with the implementation (!!! contains spoilers)](https://github.com/Magicianred/my-blog-sample/tree/pathFromV1toV2/step03/add-author-to-posts)

[Return to main page](../README.md) 

