# My Blog Sample  
([Italian translate](PostTags_IT.md))  

## Adding tags to posts [database, backend, frontend]  
Jim heard from a friend who works in SEO that tags are very handy, so he wants to add them to his blog too.  
Tom suggests creating a new table for the Tags and creating a relationship table with the Posts  

### Implementation specifications  

#### Database  
- Create a table called *Tags* with the following columns:  
  * Id * [int, primary key],  
  * Name * [string],  
  * Description * [string],  
  * CreateDate * [datetime] 
  
- Create a table called *PostTags* with the following columns:  
  * PostId  * [int, primary key], 
  * TagId  * [int, primary key], 

#### Backend  

##### Domain Project 
- Add an interface *ITag.cs* in the */Interfaces/Models* folder, use the *IPost.cs* as a trace, copy the code and adapt it, but add a property to hold the tag posts:  
```csharp
public List<Post> Posts { get; set; }
```  
- Modify the interface *IPost.cs* in the */Interfaces/Models* folder, add also a property to hold the tag posts:
```csharp
public List<Tag> tags { get; set; }
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
- Modify class *PostTagsHelper.cs* in the */Helpers* folder, add also the following method To enhance the posts with tags:
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


[TO COMPLETE]  

[Return to main page](../README.md)  
