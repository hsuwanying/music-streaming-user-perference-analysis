# Improving Music Streaming Recommader System with User Perference Analysis 
The project aims to improve recommendation system feature with the help of analysing user data. The project and data originated from Kaggle, and was submmited as part of assigment for REC course at HSLU 

## Project task:
Business background Research, Data Exploration, Feature Engnerring and Data Analysis

## Data Description
The target variable of this dataset is is_listened. There are 7'558'834 obersvations with 14 preditors
 - genre_id: identifiant of the genre of the song
 - media_id: identifiant of the song listened by the user
 - album_id: identifiant of the album of the song
 - media_duration: duration of the song
 - user_gender: gender of the user
 - user_id: anonymized id of the user
 - context_type :type of content where the song was listened: playlist, album ...
 - release_date: release date of the song with the format YYYYMMDD
 - ts_listen: timestamp of the listening in UNIX time
 - platform_name: type of os
 - platform_family: type of device
 - user_age: age of the user
 - listen_type if the songs was listened in a flow or not
 - artist_id: identifiant of the artist of the song
 - is_listened: 1 refers a track was listened, 0 otherwise

 
After the data exploration, we’ve found three main issues in the train dataset:
1. There 17 entries of released_date is 30000101, which cannot be recognized with the time format
2. 29,779 data entries where ts_listen is greater than released_date
3. There are 2 records where ts_listen is earlier than the time when Deezer was founded (in 2006) 

To better understand user preferences, behaviors and listening patterns, a series of feature engineering was conducted. Time-related features such as year, month, day, weekday, is_weekend, hour, minutes and seconds were derived from ‘ts_listen’, which indicates the time a user starts to listen to a track. After that, season and sessions were derived from month and hour, and ladled with four seasons and six different time sessions. Last, user listening patterns including ‘listen_diff’, ‘listen_percent’,  ‘time_gap’,  ‘listen_start’,  ‘listen_end’ were created by aggregating ‘user_id’, ‘ts_listen’,  ‘user_age’,  ‘media_duration’ and ‘media_id’. More detail can be seen in Deezer_eda_result.ipynb file.


### User preference analysis
Time is an essential factor which shifts users perderence from time to time. In Figure 2, user listening time in session, we found that users started listening to music in the morning, reached the peak in the afternoon, and then dropped in the evening. Figure 3 gives more detail about the variety of number of users changes hourly-based. Key findings are summarized as following:

1. Number of active users dramatically increased between 5am to 6am.
2. The highest number of listeners showed up between 4 to 6pm, with figures above 500,000.
3. The number of users constantly decreased in the evening and dropped to 200,000 at 23 pm. 

### Genre Preference analysis
When it comes to content analysis, genre is one of the features that can differ from time to time, as well as influenced by the surrounding scenarios of users. We found that there are 6 main genres, genre id 0, 7, 10 ,25, 27 and 14, were very popular among all other attributes, such as hour, session, context, platform, listen type and user_age. In other words, no matter the time, the user age or the context, these 6 genres would be favored by the users. Key findings are listed below and graphical analysis can be seen in deezer_eda_result.ipynb - Genre Analysis :

1. Genre_id 0 was the most popular genre among the top 10 ranking.
2. Genre_id 0, 7, 10 ,25, 27, 14, 734, 297, 2744 were the most popular.
3. Popular genres are beloved across most sessions. Except that genre_id 2744 was not popular during night and midnight, genre_id 50 was preferable during 4. the Night, and genre_id 3645 in the midnight.
5. The Number of users listening to genre 0 was four times more without listening in the flow, whereas, there were more variety genres appearing when 6. users were listening in the flow.
7. Genre preference was different between user age groups. Among that, gerne_id 0 domainted genre preference across all user age groups, while user age 19 8. is the main audience of this genre.

### User listening pattern analysis based on user age

Attributes ‘user_id’, ‘user_age’, ‘media_id’ (songs) were aggregated for calculating average number of songs listened per user and the percentage of songs listened across each user age group. The result is summarized as below:

1. The number of songs, the length of songs and song listened percentage increased gradually as the age rises.
2. Young users were more likely to skip songs than the 30-year-old age group.
3. Users with a 30 year-old age were more likely to finish songs recommended by the system.
4. Users aged 30 listened to nearly two times more songs than users aged above 20.
5. Majority of users listening in the flow skipped more songs than users who were not in a flow, except users aged 19 and 30 

To sum up, we found that time is one of the critical elements that can affect the user when it comes to listening type of songs. Music preference also changed differently between user age groups, platform, and listen environments. To improve the new service FLOW and reduce user bouncing rate, a context-based recommendation system is suggested, nevertheless, personalized features need to be considered when building such a model.

## Reflection

It was a great experience to work on a dataset which contains millions of entries. Ideally, it would be good to start data processing in a database due to the simplicity of programming. In addition,  performing data queries can help us to have a quick glance of data and have better understanding when performing some statistical calculations. 

On the other hand, there are many categorical attributes which are replaced with numeric labels in the given dataset; it would be helpful to have the original labels of each categorical variable, which can help analysts form problem statements or hypotheses as well as provide better interpretation when analyzing data.
