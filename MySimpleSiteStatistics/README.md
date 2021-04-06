# My Simple Site Statistics
([Italian translate](README_IT.md))

## Index

- [Preface](#preface)
- [Instructions](#instructions)
- [Clone the repository](#clone_the_repository)  
- [Features to implement](#features-to-implement)    
        - [Add more view of data visualization [database]](#add_more_view_of_data_visualization)    
        - [Add others stored procedure of insertion [database, unit test]](#add_stored_procedure_of_insertion)   
  
## Preface

Mark is developping a system for registrartion of the accesses to websites.  
To implement that he created several tables to store data, some stored procedure to insert them and the views for facilitate of visualization.  

Jacob, a colleague of Tom, who is interested to the project, asked a for a series of features for adding to the project to implement it in its own blog and finally having a way to find out how many accesses receives its own site.  

Mark who given the unexpected feature request, needs help. Jacob suggested your name and now Mark asked you to implement some of the features.    

## Instructions

Below you will find lisetd the features that will be implemented in the project. It will be presented a *functional* description which is what the *customer*, in our case Jacob, wants to have it on his blog. If you have some experience, or you want get involved, this description may be enough for you to start asset. On the contrary if you need help figuring out what to do, click on the link *Implementation specifications* and you will find the technical details on how to proceed.  

## Clone the repository

To get start clone the project repository  
```bash
git clone https://github.com/Magicianred/my-simple-site-statistics-mssql.git
```
## Features to implement  
The features to be implemented will lead to the release of version 1.0 of the project.  

## Add more view of data visualization  

*[database]*  
To build a dashboard where to view the access statistics, it has been noticed that making simple queries for each table is inefficient and it would be useful to create VIEWs that allow you to optimize performance and have a more complete data for each request.  

The dashboard will present these statistics:  
- List of visits by time period (by day) and by website. The following data will be displayed: Reference period, website, number of views.    
- List of visits by time period (by day) and by page, filtered by website. The following data will be displayed: Reference period, page viewed, number of views.  
- List of visits by time period (by day) and by browser, filtered by website. The following data will be displayed: Reference period, browser (user agent string), number of views.  
- List of visits by time period (by day) and by user, filtered by website. The following data will be displayed: Reference period, user, number of views.  

[Implementation specifications](Features/AddViews.md)  

[Learning Goal](LearningGoals/AddViews.md)  

## Add stored procedure of insertion  

*[database, unit test]*  
Currently for insertion of access (site visits - accesses_visites) simple sql INSERTs are made, some need to check if the data is already present before insertion, to avoid duplicates. This involves execution of one or more queries for each operation and leave this task to the Backend is less efficient because the request passes from the backend to the database several times, generating traffic and delays. For this it is convenient to create a series of stored procedures to make everything more performing.  

This may require a single stored procedure, the one relating to accesses_visites, but it is useful to break it down to be able to use it in other parts of the application as well.  

In addition of the one already present, to insert the browser accesses it is necessary to create the following:  

- *accesses_ip*
- *accesses_pages* (which must also check the reference websites)
- *accesses_visites* (which must also the pages, the current one and the referrer, browser and the user)  


[Implementation specifications](Features/AddStoredProcedures.md)  

[Learning Goal](LearningGoals/AddStoredProcedures.md)

