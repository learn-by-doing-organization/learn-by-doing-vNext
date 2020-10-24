# My Blog Sample  
([Italian translate](README_IT.md))

# My Blog Sample  

## Preface  
Jim and Tom are two friends that have decided to start a blog.  
Jim is always full of ideas and involved Tom, who is a programmer always too busy, in the realization of this personal project.  

Tom wanted to help his friend, but having little time, he left the project unfinished.  
Jim was not discouraged, however, and with one of his ideas he found a way to carry on the project: searching on the web he found you and asked you for help for his blog. He knows that you are not an expert programmer, but with some Tom's indications about how to proceed there will be no problem!  

The code of the project is very structured, but it has few features yet. It is ready for testing, but the current ones doesn't make much sense, but they are in any case an excellent basis for creating new ones.  

## Instructions
Below you will find listed the features them will want to see implemented in the project. A *functional* description will be presented which is what the *customer*, in our case Tom and Jim, want to have on their blog. If you have some experience, or want to get involved, this description may already be enough for you to start the business. On the contrary, if you need help understanding what to do click on the link *Implementation specifications* and you will find technical details on how to proceed.  

## Features to implement  
The features to be implemented will lead to the release of version 2.0 of the project.  

### Add categories to Posts [database, backend, frontend]  
Jim wants to create logical categories to collect the Posts. He would like the Posts to be linked to a category, for now he doesn't mind being able to link them to more than one category, only one is enough.  
Tom suggests inserting a new table for the categories and adding a reference to the category in the Post table.  

[Implementation specifications](Features/PostCategories.md)  

### Adding Tags to Posts [database, backend, frontend]  
Jim heard from a friend, who works in SEO, that tags are very handy, so he wants to have them on his blog too.  
Tom suggests creating a new table for the Tags and creating a relationship table with the Post table.  

[Implementation specifications](Features/PostTags.md)  

### Adding the Author to Posts [database, backend, frontend]  
Jim would like to involve other friends to write the blog posts, so he needs to indicate in the posts who is the author. At the moment he does not think it is necessary to create the Authors entity, it will be enough to indicate the author.  
Tom suggests adding an Author field in the Posts table.  

[Implementation specifications](Features/PostAuthor.md)  

### Add pagination to the Post list [backend, frontend]  
Jim already knows that the blog will be full of posts and he doesn't want them all to be visible on the first page.  
Tom suggests inserting pagination to the *Index* action of the *HomeController* controller in order to allows to show only 3 posts at a time.  

[Implementation specifications](Features/PostPagination.md)  

### Correcting the test [backend, testing]  
Tom realized that he changed the UI of the web project, but didn't fix the *should_retrieve_all_posts* test of the *Magicianred.LearnByDoing.MyBlog.Web.Tests.Integration* project that now it reported an error.  

[Implementation specifications](Features/ErrorInTest.md)   

## Nice To Have (NTH)  
NTH features are not expected in the release 2.0 of the project, but will likely be implemented in version 3.0.  

### A new User Interface [frontend]  

[Implementation specifications](Features/NewUI.md)  

### Using a modern framework for the frontend [frontend + javascript]  

[Implementation specifications](Features/ClientFramework.md)  