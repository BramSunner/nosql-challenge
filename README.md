# About the Project
This project consists of two parts: setup and analysis.  

### Setup

In this part, I establish a MongoDB database using pymongo given a json file to import.  
I establish a connection to MongoDB.  
Then, I create an empty database titled 'uk_food' (Note: the code deletes prior databases of the same name if in existence).  
After, I create a collection titled 'establishments' (Note: the code deletes prior collections of the same name but this should never be an issue).  
I load the json file and then input it into the collection.  
As a final check, I find one document in the database and see if the setup has been done correctly.  

After the intial setup, there are some requested changes to the database.  
First, a new restaurant is to be added to the collection.  
This is provided in a dictionary and inserted into the collection.  
This article's 'BusinessTypeID' is updated to match the other restaurants of the same type.  
Another change is to delete all articles whose LocalAuthorityName is "Dover".  
Lastly, a series of updates to existing entries must be made.  
The RatingValue, longitude, and latitude need to be changed to numeric data.  
Both the longitude and latitude are changed to a float, and the RatingValue is changed to an integer.  
(Note: some of the prior RatingValues were non-numeric, "Pass" or "Exempt", etc., and those values are changed to None).  
After all updates are confirmed to have worked, this part of the project is finished.  

### Analysis

In this part, I establish a connection to the uk_food database with pymongo again.  

This time, I have four questions to answer using database queries:  
1. ### Which establishments have a hygiene score equal to 20?  

This is achieved via a simple count given a query searching for hygiene scores equal to 20.  
   
2. ### Which establishments in London have a RatingValue greater than or equal to 4?  

This is achieved, again, via a simple count given a query searching for RatingValues greater than or equal to 4.  
   
3. ### What are the top 5 establishments with a RatingValue rating value of 5, sorted by lowest hygiene score, nearest to the new restaurant added, "Penang Flavours"?  

For this question, the query is a bit more complex.  
It searches for entries whose:  
- Latitude is greater than or equal to Penang Flavours latitude minus .01 (the area to be searched).  
- Latitude is less than or equal to Penang Flavours latitude plus .01.  
- Longitude values matching the same logic in 1 and 2.  
- And with a RatingValue of 5.

The results are limited to 5 and sorted by hygiene scores descending.  

4. ### How many establishments in each Local Authority area have a hygiene score of 0?  

This question is answered using an aggregation.  
I find entries whose hygiene scores are 0.  
These entries are grouped into groups based on their 'LocalAuthorityName'.  
The entries are also counted using a 'sum' aggregation.  
I sort the entries by their count.  

For each of the questions, the results are made into a pandas DataFrame and the top ten results are shown (5 for part 3). 

# Built In
Python.  
Jupyter Notebook.  
MongoDB.  
