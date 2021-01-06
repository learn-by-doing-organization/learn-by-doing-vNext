# My Blog Sample
([Italian translate](README_IT.md))

## Index

- [Preface](#preface)  
- [Instructions](#instructions)  
- [Features to implement](#features-to-implement)  
    - [Add categories to Posts [database, backend, frontend]](#add-categories-to-posts)
        - [Implementation specifications](Features/PostCategories_IT.md) 
        - [Learning goals](LearningGoals/PostCategories_IT.md)  
    - [Adding Tags to Posts [database, backend, frontend]](#adding-tags-to-posts)
        - [Implementation specifications](Features/PostTags_IT.md) 
        - [Learning goals](LearningGoals/PostTags_IT.md)  
    - [Adding the Author to Posts [database, backend, frontend]](#adding-the-author-to-posts)
        - [Implementation specifications](Features/PostAuthor_IT.md) 
        - [Learning goals](LearningGoals/PostAuthor_IT.md)  
    - [Add pagination to the Post list [database, backend, frontend]](#add-pagination-to-the-post-list)
        - [Implementation specifications](Features/PostPagination_IT.md) 
        - [Learning goals](LearningGoals/PostPagination_IT.md)  
    - [Final test, test fix and known bug fixes [backend, frontend, testing]](#final-test,-test-fix-and-known-bug-fixes)
        - [Implementation specifications](Features/BugFixing_IT.md) 
        - [Learning goals](LearningGoals/BugFixing_IT.md)  
- [Nice To Have (NTH)](#nice-to-have-(nth))  
    - [A new User Interface (UI) [frontend]](#a-new-user-interface-(ui))  
    - [Using a modern framework for the frontend [frontend + javascript]](#using-a-modern-framework-for-the-frontend)  

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

### Add categories to Posts
*[database, backend, frontend]*  
Jim wants to create logical categories to collect the Posts. He would like the Posts to be linked to a category, for now he doesn't mind being able to link them to more than one category, only one is enough.  
Tom suggests inserting a new table for the categories and adding a reference to the category in the Post table.  

[Implementation specifications](Features/PostCategories.md)  

[Learning goals](LearningGoals/PostCategories.md)  

### Adding Tags to Posts
*[database, backend, frontend]*  
Jim heard from a friend, who works in SEO, that tags are very handy, so he wants to have them on his blog too.  

Tom suggests creating a new table for the Tags and creating a relationship table with the Post table.  

[Implementation specifications](Features/PostTags.md)  

[Learning goals](LearningGoals/PostTags.md)  

### Adding the Author to Posts
*[database, backend, frontend]*  
Jim would like to involve other friends to write the blog posts, so he needs to indicate in the posts who is the author. At the moment he does not think it is necessary to create the Authors entity, it will be enough to indicate the author.  
Tom suggests adding an Author field in the Posts table.  

[Implementation specifications](Features/PostAuthor.md)  

[Learning goals](LearningGoals/PostAuthor.md)  

### Add pagination to the Post list
*[backend, frontend]*  
Jim already knows that the blog will be full of posts and he doesn't want them all to be visible on the first page.  
Tom suggests inserting pagination to the *Index* action of the *HomeController* controller in order to allows to show only 3 posts at a time.  

[Implementation specifications](Features/PostPagination.md)  

[Learning goals](LearningGoals/PostPagination.md)  

### Final test, test fix and known bug fixes
*[backend, frontend, testing]*  
Jim asked Tom to take a look at the site because there seems to be some problems.

Tom realized that he changed the UI of the web project, but he didn't fix the *should_retrieve_all_posts* test of the *Magicianred.LearnByDoing.MyBlog.Web.Tests.Integration* project which now reports an error.  
Also an error has been reported in retrieving posts by tag. It seems that all posts are always recovered, you have to check and fix the problem.  
Tom also asked you to help him check for other bugs. If you find any, please report it on GitHub and, if you want, help solve it.  

[Implementation specifications](Features/TestingAndBugFixing.md)  

[Learning goals](LearningGoals/TestingAndBugFixing.md)  

## Nice To Have (NTH)
NTH features are not expected in the release 1.0 of the project, but will likely be implemented in version 2.0.  

### A new User Interface (UI)
*[frontend]*  
Jim feels the need, also requested by many blog users, to have a better UI for the use of the blog. Something more "beautiful", "modern" and "captivating".  

### Using a modern framework for the frontend
*[frontend + javascript]*  
Jim visited friends' blog and saw that they use more dynamic frontend visualization techniques. There is no need to reload the page with each click and everything seems smoother, like a Desktop application. Tom explained to Jim that we need to introduce a modern framework to visualize the interface and improve the web api that are currently present in the application.
