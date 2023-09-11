# NoSQL-Challenge

The UK Food Standards Agency evaluates various establishments across the United Kingdom, and gives them a food hygiene rating.
For this challenge I was contacted by the editors of a food magazine, Eat Safe, Love, because they wanted me to evaluate some of 
the ratings off a dataset in order to help them and food critics decide where to best focus future articles. 

This challenge was divided into three parts:

-- Part 1: Database and Jupyter Notebook Set Up

I had to Import the data provided in the establishments.json file from my Terminal. Name the database uk_food and the collection establishments. 
Copy the text I used to import the data from my Terminal to a markdown cell in your notebook. Within my notebook, import the libraries that I needed: 
PyMongo and Pretty Print (pprint). Create an instance of the Mongo Client. Confirmed that I created the database and loaded the data properly:

Listed the databases in MongoDB and then confirm that uk_food is listed. Afterwards List the collection(s) in the database to ensure that establishments is there.
Found and displayed one document in the establishments collection using find_one and display with pprint. Lastly Assigned the establishments collection to a variable 
and prepared the collection for use.

-- Part 2: Update the Database
NoSQL_setup_starter.ipynb was used for this section of the challenge.

The magazine editors made some requests for modifications for the database before I could perform any queries or analysis for them. 
I had to make the following changes to the establishments collection:

Adding an exciting new halal restaurant just opened in Greenwich but hasn't been rated yet. The magazine asked me to include it in my analysis 
by adding the following information to the database:

{
    "BusinessName":"Penang Flavours",
    "BusinessType":"Restaurant/Cafe/Canteen",
    "BusinessTypeID":"",
    "AddressLine1":"Penang Flavours",
    "AddressLine2":"146A Plumstead Rd",
    "AddressLine3":"London",
    "AddressLine4":"",
    "PostCode":"SE18 7DY",
    "Phone":"",
    "LocalAuthorityCode":"511",
    "LocalAuthorityName":"Greenwich",
    "LocalAuthorityWebSite":"http://www.royalgreenwich.gov.uk",
    "LocalAuthorityEmailAddress":"health@royalgreenwich.gov.uk",
    "scores":{
        "Hygiene":"",
        "Structural":"",
        "ConfidenceInManagement":""
    },
    "SchemeType":"FHRS",
    "geocode":{
        "longitude":"0.08384000",
        "latitude":"51.49014200"
    },
    "RightToReply":"",
    "Distance":4623.9723280747176,
    "NewRatingPending":True
}

I then had to find the BusinessTypeID for "Restaurant/Cafe/Canteen" and return only the BusinessTypeID and BusinessType fields.
Update the new restaurant with the BusinessTypeID I found.

The magazine expressed that they were not interested in any establishments in Dover, so I checked how many documents contained the Dover Local Authority. 
Then, removed any establishments within the Dover Local Authority from the database, and checked the number of documents to ensure they were deleted.
Some of the number values are stored as strings, when they should be stored as numbers. So I Used update_many to convert latitude and longitude to decimal numbers.
Used update_many to convert RatingValue to integer numbers.

-- Part 3: Exploratory Analysis
Eat Safe, Love has specific questions they wanted me to answer, which would help them find the locations they wished to visit and avoid.

The NoSQL_analysis_starter.ipynb was also used for this section of the challenge.

There were some notes that I needed to be aware of:

The RatingValue refers to the overall rating decided by the Food Authority and ranges from 1-5. The higher the value, the better the rating.
This field also includes non-numeric values such as 'Pass', where 'Pass' means that the establishment passed their inspection but wasn't given a number rating. 
I had to coerce non-numeric values to nulls during the database setup before converting ratings to integers.
The scores for Hygiene, Structural, and ConfidenceInManagement work in reverse. This means, the higher the value, the worse the establishment is in these areas.
I Used the following questions to explore the database, and find the answers, so I could provide them to the magazine editors.

Unless otherwise stated, for each question:

- I Used count_documents to display the number of documents contained in the result.

- Displayed the first document in the results using pprint.

- Converted the result to a Pandas DataFrame, printed the number of rows in the DataFrame, and displayed the first 10 rows.

- Looked at Which establishments had a hygiene score equal to 20 and Which establishments in London had a RatingValue greater than or equal to 4.

- Looked at What were the top 5 establishments with a RatingValue of 5, then sorted by lowest hygiene score, nearest to the new restaurant added, "Penang Flavours"?

- Lastly How many establishments in each Local Authority area had a hygiene score of 0? Sorted the results from highest to lowest, and printed out the top ten local authority areas.

*Technologies used: Microsoft Visual Studio Code.
