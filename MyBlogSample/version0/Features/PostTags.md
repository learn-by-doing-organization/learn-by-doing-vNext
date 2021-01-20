# My Blog Sample
([Italian translate](PostTags_IT.md))  

## Adding tags to posts [database, backend, frontend]
Jim heard from a friend who works in SEO that tags are very handy, so he wants to add them to his blog too.  

Tom suggests creating a new table for the Tags and creating a relationship table with the Posts.  

### Implementation specifications

#### Database
- Create a table called *Tags* with the following columns:  
  - *Id* [int, primary key],  
  - *Name* [string],  
  - *Description* [string],  
  - *CreateDate* [datetime] 
  
- Create a table called *PostTags* with the following columns:  
  - *PostId* [int, primary key],  
  - *TagId* [int, primary key]  

#### Backend

##### Domain Project
- Add an interface *ITag.cs* in the */Interfaces/Models* folder, use the *IPost.cs* as a trace, copy the code and adapt it, but add a property to hold the tag posts:  
```csharp
public List<Post> Posts { get; set; }
```  
- Modify the interface *IPost.cs* in the */Interfaces/Models* folder, add also a property to hold the tag posts:  
```csharp
public List<Tag> Tags { get; set; }
```  
- Add an interface *IPostTag.cs* in the */Interfaces/Models* folder, use the *IPost.cs* as a trace, copy the code and adapt it.  
- Add an interface *ITagsRepository.cs* in the */Interfaces/Repositories* folder, use the *IPostsRepository.cs* as a trace, copy the code and adapt it.  
- Add an interface *ITagsService.cs* in the */Interfaces/Services* folder, use the *IPostsService.cs* as a trace, copy the code and adapt it.  
- Add a class *Tag.cs* in the */Models* folder, use the *Post.cs* as a trace, copy the code and adapt it.  
- Add a class *PostTag.cs* in the */Models* folder, use the *Post.cs* as a trace, copy the code and adapt it.  

##### UnitTest DAL project (optional, but highly recommended)
- Add a class *Tag.cs* in the */Models* folder, use the *Post.cs* class as a trace, copy the code and adapt it.  
- Add a class *PostTag.cs* in the */Models* folder, use the *Post.cs* class as a trace, copy the code and adapt it.  
- Add a class *PostTagsHelper.cs* in the */Helpers* folder, use the *PostsHelper.cs* class as a trace, copy the code and adapt it.  
- Modify class *PostsHelper.cs* in the */Helpers* folder, add also the following method To enhance the posts with tags:  
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
- Add a class *TagsHelper.cs* in the */Helpers* folder, use the *PostsHelper.cs* class as a trace, copy the code and adapt it. such as *PostsHelper.cs* create a method 
*GetMockDataWithPosts* to obtain tags of Posts.  
- Add a test in class *PostsRepositoryTest.cs* in the /Repositories folder, use the test *should_retrieve_post_by_id* as a trace, copy the code and adopt it to verify the retriew of tags in post.  
(To work correctly the InMemory database you have to insert first the Tag and the PostTag and then the Post with tag inside. If you don't do this you will receive an error saying "There is not table *Tags* or *PostTags* in the database". Make this correction  also in the method *should_retrieve_all_posts*)  
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
- Add a class *TagsRepositoryTest.cs* in the */Repositories* folder, use the class *PostsRepositoryTest.cs* as a trace, copy the code and adopt it.  

###### Be careful, in the *TagsRepositoryTest.cs* class use the *Tag * and *PostTag * class you created in this project, not the *Domain* project one. This is an exception due to the InMemory database not recognizing the table name correctly, with this *hack* you can pass the table name through the *Tag* class attribute, or in your implementation *Tag* (Tom is still working to solve this case correctly).

```csharp
[Alias("Tags")]
``` 
###### Be careful, the test project doesn't compile because there are no class in DAL Project. It's ok, in TDD practice you write before the test and then you write code for use it.

##### DAL Project
- Modify *PostsRepository.cs* class in the */Repositories* folder and retrieve all tags of post in the property:  
```csharp
public List<Tag> Tags  { get; set; }
```  
- Add *TagsRepository.cs* class in */Repositories* folder, use *PostsRepository.cs* class as trace, copy the code and adapt it, but remember to retrieve all posts of the tag in the property:  
```csharp
public List<Post> Posts { get; set; }
```  

###### Be careful, Dapper can't retrieve the priperty of type *List*, so you have to indicate all the values of Projection in query, for ex:
```sql
SELECT Id, Name, Description FROM Tags
```  

##### UnitTest BL (optional, but highly recommended)
- Add *TagsHelper.cs* class in */Helpers* folder, use *PostsHelper.cs* class as trace, copy the code and adapt it.  
- Add *TagsServiceTest.cs* class in */Services* folder, use *PostsServiceTest.cs* class as trace, copy the code and adapt it.  
- Add some other tests to verify retrieve the Tag of Post or the Post of Tag.  

##### BL Project
- Add the *TagsService.cs* class in the */Services* folder, use the *PostsService.cs* class as a trace, copy the code and adapt it.  

####  Web Project
- Add the *Tags* action in the *HomeController* controller, use the *Index* action as a trace, copy the code and adapt it.  
- Add the *Tag({id})* action in the *HomeController* controller, use the *Post({id})* action as a trace, copy the code and adapt it.  
- Add the *Tags* view in the *Views/Home* folder, use the *Index* view as a trace, copy the code and adapt it.  
- Add the *Tag* view in the *Views/Home* folder, use the *Post* view as a trace, copy the code and adapt it, but remember that you will also have to display the list of posts contained in the tag, for this you can see the *foreach* in the *Index* view.  
- Add a link to Categories page in *Views/Shared/_Layout.cshtml*, you can copy and past the link Home and adapt it.  
```razor
<a href="@Url.Action("Tags", "Home")" data-rb-event-key="about" class="nav-link">Tags</a>
``` 
- In *Startup.cs* file, add code to handle dependency injection for the new interfaces and classes, inside the function *ConfigureServices*:  
```csharp
services.AddScoped<ITag, Tag>();
services.AddScoped<IPostTag, PostTag>();
services.AddScoped<ITagsRepository, TagsRepository>();
services.AddScoped<ITagsService, TagsService>();
```  

#### Integration Test Web Project
- Add a test like *HomeControllerTest.should_retrieve_all_posts* to verify that the tag page responds correctly.  
- Add a test like *HomeControllerTest.should_retrieve_post_by_id* to verify that the page of detail of tag responds correctly when requesting an existing id.  
- Add a test like *HomeControllerTest.should_retrieve_no_one_post* to verify that the page of detail of tag responds correctly when requesting a non-existent id.  

[See the repository with the implementation (!!! contains spoilers)](https://github.com/Magicianred/my-blog-sample/tree/pathFromV1toV2/step02/add-tags-to-posts)  

[Return to main page](../README.md)  

