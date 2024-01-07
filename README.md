# nosql-challenge
# Eat Safe And Love.

Module 12 Challenge filesLinks to an external site.

# Background

The UK Food Standards Agency evaluates various establishments across the United Kingdom, and gives them a food hygiene rating. WE have been contracted by the editors of a food magazine, Eat Safe, Love, to evaluate some of the ratings data in order to help their journalists and food critics decide where to focus future articles.
We divided our Task into three parts
1. Database and Jupyter Notebook Set Up.
2.  Update the Database.
3.  Exploratory Analysis.
    
 ### Required Libraries:
from PyMongo import MongoClient
from PPrint import pprint
import Pandas 

## Part 1: Database and Jupyter Notebook Set Up
We created  NoSQL_setup_starter.ipynb for this section of the challenge.
Imported the data provided in the establishments.json file from Terminal. 
Created the database uk_food and the collection establishments.
syntax is:
###### 'mongoimport -type json -d uk_food -c establishments --drop --jsonArray establishments.json'

Create an instance of the Mongo Client.
### mongo = MongoClient(port=27017)

Check to conform we created database and loaded the data properly.
List the databases in MongoDB. Confirm that uk_food is listed.
List the collection(s) in the database to ensure that establishments is there.

Find and display one document in the establishments collection using find_one and display with pprint.

Assign the establishments collection to a variable to prepare the collection for use.
#### establishments = db['establishments']

## Part 2: Update the Database
Used NoSQL_setup_starter.ipynb for this section of the challenge.

The magazine editors have some requested modifications for the database before you can perform any queries or analysis for them. Make the following changes to the establishments collection.
1.An exciting new halal restaurant just opened in Greenwich, but hasn't been rated yet. The magazine has asked you to include it in your analysis. Add the following restaurant "Penang Flavours" to the database.


2.Find the BusinessTypeID for "Restaurant/Cafe/Canteen" and return only the BusinessTypeID and BusinessType fields.


3.Updated the new restaurant with the BusinessTypeID you found.


4.The magazine is not interested in any establishments in Dover, so check how many documents contain the Dover Local Authority( i.e: 994). Then, remove any establishments within the Dover Local Authority from the database, and check the number of documents to ensure they were deleted.

5. Some of the number values are stored as strings, when they should be stored as numbers.

Use update_many to convert latitude and longitude to decimal numbers.
Use update_many to convert RatingValue to integer numbers.


## Part 3: Exploratory Analysis
Eat Safe, Love has specific questions they want you to answer, which will help them find the locations they wish to visit and avoid.

Use NoSQL_analysis_starter.ipynb for this section of the challenge.
#### hints
Some notes to be aware of while you are exploring the dataset:

RatingValue refers to the overall rating decided by the Food Authority and ranges from 1-5. The higher the value, the better the rating.

Note: This field also includes non-numeric values such as 'Pass', where 'Pass' means that the establishment passed their inspection but isn't given a number rating. We will coerce non-numeric values to nulls during the database setup before converting ratings to integers.
The scores for Hygiene, Structural, and ConfidenceInManagement work in reverse. This means, the higher the value, the worse the establishment is in these areas.


1.Which establishments have a hygiene score equal to 20? (41 of them)
![image](https://github.com/svuth23/nosql-challenge/assets/136966712/8006695d-06dc-47d1-98b5-4d209bd54607)

2.Which establishments in London have a RatingValue greater than or equal to 4?

![image](https://github.com/svuth23/nosql-challenge/assets/136966712/6ad454ed-e9cf-42c6-8d55-3f584fa6711e)

Hint: The London Local Authority has a longer name than "London" so you will need to use $regex as part of your search.

3. are the top 5 establishments with a RatingValue of 5, sorted by lowest hygiene score, nearest to the new restaurant added, "Penang Flavours"?

Hint: You will need to compare the geocode to find the nearest locations. Search within 0.01 degree on either side of the latitude and longitude.

result is : 
![image](https://github.com/svuth23/nosql-challenge/assets/136966712/871d1b62-0286-4881-8391-c714077c757b)

4.How many establishments in each Local Authority area have a hygiene score of 0?i.e 55.
Sort the results from highest to lowest, and print out the top ten local authority areas.

Hint: You will need to use the aggregation method to answer this.

The first 5 rows of your resulting DataFrame :

![image](https://github.com/svuth23/nosql-challenge/assets/136966712/5ac478b9-7b5a-48f0-808c-71a2412b7317)


