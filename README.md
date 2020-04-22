# WeRateDogs_Project

The goal of this project is to wrangle WeRateDogs Twitter data to create interesting and trustworthy analyses and visualizations.
The Twitter archive is great, but it only contains very basic tweet information.
Additional gathering, then assessing and cleaning is required for "Wow!"-worthy analyses and visualizations.

The goals of this project were:

1)	Gathering Data from three different sources
2)	Assessing the Data both Visually and Programmatically
3)	Cleaning the Data programmatically
4)	Storing the Analyzed the data into a file in .csv format
5)	Finally using the cleaned data to draw insights through visualization

# Gathering Data

The first step in the data wrangling process is Gathering data. Here I gathered data by three different means:

1)	Manually uploading the file  twitter_archive_enhanced.csv 
2)	Programmatically downloading the file image_predictions.tsv from the Udacity Servers 
3)	Using the Tweepy library to gather tweet data in JSON format tweet_json.txt, finally reading this text file data into a pandas dataframe

# Assessing Data:

The Quality Issues and Tidiness Issues identified through assessment are:

Quality issues

1)	Data contains retweets --> retweeted_status_id for some rows is not NAN, hence duplicate data is present.
2)	No of records in img_predictions table does not match with df_tweets table
3)	No of records in df_tweets table does not match with twitter_archive table
4)	No of records in img_predictions table does not match with twitter_archive table
5)	Datatype issues in all three tables, the timestamps are not in format datetime
6)	source column in twitter archive contains unncessary html tags.
7)	Values in the name column - some lowercase, some start with uppercase, there are some invalid names like 'a' or are they valid names?
8)	The denominator ratings in twitter_archive table are >10 and the numerator ratings seem errenous
9)	Multiple columns in image predictions table about the right breed name for the dog in the image


Tidiness

1)	Removing columns -> empty values in retweet_status_id and retweet_status_userid hence, these columns to be dropped
2)	doggo, pupper, puppo should all be merged into one single column 'growth_stage'
3)	Need to drop doggo, pupper, puppo, floofer columns
4)	Need to drop the columns p1,p2,p3,p1_dog,p2_dog,p3_dog,p1_conf,p2_conf,p3_conf
5)	Merge all three tables together to create a single dataset twitter_archive table, image_predictions tables and df_tweets table

# Cleaning Data

Firstly, a copy of all the datasets were made.

Addressing Quality Issues:

1)	Cleaned data in arc_clean to only have original tweets - no retweets
2)	(2,3,4) Cleaned to have consistent data across all three tables - arc_new, df_new, img_pred_new by removing mismatched records, keeping only those present in all three tables
3)	Corrected datatype issues in all three tables, converting to datetime format
4)	Removed the html tags from the source column
5)	Replace all inaccurate names like ‘a’,’an’,’him’ etc., as None
6)	Created a new column rating to correct errenous values in rating_numerator and rating denominator
7)	Created a new image predicted column based on the confidence levels of the images given

Addressing Tidiness Issues

1)	Removed the unnecessary columns in arc_clean table -- in_reply_to_status_id,in_reply_to_user_id,retweeted_status_id,retweeted_status_user_id,retweeted_status_timestamp
2)	Merged the columns, doggo, pupper, floofer and puppo into a single column which is growth_stage
3)	Dropped the extra columns - doggo, floofer, pupper, puppo
4)	Dropped columns rating_numerator and rating_denominator as it is not necessary anymore
5)	Removed the columns p1,p2,p3,p1_conf,p2_conf,p3_conf,p1_dog,p2_dog,p3_dog
6)	Merged all datasets to create one single dataset

Finally, the merged dataset was written into a new .csv file called twitter_master_archive.csv

# Analyzing & Visualizing Data

In Analyzing and Visualizing data, the following observations were made:

1)	The degrees of correlation between retweet_count, followers_count, favorite_count
2)	We can find the source from which users have tweeted the most
3)	We can find what is the popular dog stage of our dog lovers

4)	We can find which is the most popular breed of dog amongst our dog lovers
5)	Using tweet_create_date we can see when or what time of day our dog lovers are most active at.
