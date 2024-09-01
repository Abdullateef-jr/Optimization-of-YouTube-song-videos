# Song Analysis in Power BI 📈💻🎵

## Table of Contents
1- [Project Overview](#project-overview)

2- [The Dataset](#the-dataset)

3- [Tool](#tool)

4- [Data Preparation](#data-preparation)

5- [Data Modelling](#data-modelling)

6- [The Analysis](#the-analysis)

7- [Insights](#insights)

8- [Recommendations](#recommendations)

9- [Limitation](#limitation)

10- [Reference](#reference)



## Project Overview

This project focused on analyzing YouTube song videos to uncover key factors that influence viewer engagement and content discoverability. Leveraging data from T-Series YouTube channel, the analysis aimed to identify trends, preferences, and patterns that could inform content creators and stakeholders on how to optimize their video releases for maximum impact.

The project explored various elements such as video quality, timing of releases, video duration, and the strategic use of tags and captions. By examining these factors, the analysis provided actionable insights into how to enhance viewer retention, increase engagement rates, and improve overall discoverability on the platform.

Key recommendations included prioritizing high-definition (HD) video releases, scheduling content during peak engagement hours, particularly in the mornings and weekends, and using a balanced approach to tagging and captioning that avoids over-reliance on generic terms. The project also highlighted the importance of fostering community interaction through interactive content like live streams and Q&A sessions.

Through this analysis, the project aimed to equip content creators and stakeholders with the tools and strategies needed to optimize their YouTube song videos for greater success in a competitive digital landscape.



![Medium first](https://github.com/user-attachments/assets/68283e6c-cf47-42e3-a9bc-7565bdcb2acc)


## The Dataset


The dataset contains key attributes such as video ID, channel title, title, description, tags, published date, view count, like count, favorite count, comment count, video duration, video definition, and caption details. Dataset Description
1. video_id: Unique identifier for each YouTube video.
2. channelTitle: Title of the YouTube channel publishing the song.
3. title: Title of the YouTube song video.
4. description: Description provided for the YouTube song video.
5. tags: Tags associated with the YouTube song video.
6. publishedAt: Date and time when the YouTube song video was published.
7. viewCount: Number of views received by the YouTube song video.
8. likeCount: Number of likes received by the YouTube song video.
9. favoriteCount: Number of times the YouTube song video has been marked as a favorite.
10. commentCount: Number of comments posted on the YouTube song video.
11. duration: Duration of the YouTube song video.
12. definition: Video definition or quality (e.g., HD, SD).
13. caption: Availability of captions for the YouTube song video.

Get the dataset [here](https://github.com/Abdullateef-jr/Optimization-of-YouTube-song-videos/blob/main/songs.xlsx)

## Tool
- Microsoft Power BI [Download here](https://medium.com/r/?url=https%3A%2F%2Fwww.microsoft.com%2Fen-us%2Fpower-platform%2Fproducts%2Fpower-bi%2Fdesktop)

## Data Preparation
Data preparation is the process of preparing raw data for further processing and analysis, including steps like data collection, cleaning, and transformation. ETL is employed in the dataset preparation.

## Data cleaning and Transformation steps
After importing the dataset, the transformation and cleaning are done in Power Query. During the transformation process, I ;
- Checked for irregularities
- Replaced null value with N/A "not available" in the description column
- Employed Title case naming convention for the column names
- Checked and replaced with the correct data type
- Added a new "Title" column with clean text
- Added a new Published_date, and year column
- Added a new "Title" column with clean text
- Time and time category column
- Added new column Duration category
- Added new column Engagement.

## Data Modelling
Data modeling is the process of creating a visual representation of a system's data elements and the relationships between them. It serves as a blueprint for how data is structured, stored, and managed in databases, applications, or information systems. Data modeling ensures efficient data retrieval, analysis, and reporting.

In the data modeling, I understood clearly the relationships between the columns and the context of the calculation to be carried out to have an accurate and in-depth analysis. This led to the addition of calculated columns and measures like;

### Total views
```DAX
Total_views = SUM('Song Analysis'[View_count])
```
### Engagement rate
``` Engagement_rate =
DIVIDE(SUM('Song Analysis'[Like_count])+SUM('Song Analysis'[Comment_count]),SUM('Song Analysis'[View_count])) * 100
```
### Growth rate
``` Engagement Growth_rate = 
VAR Current_Engagement= SUM('Song Analysis'[Engagement])
VAR Previous_Engagement=
CALCULATE(SUM('Song Analysis'[Engagement]),
DATEADD('Song Analysis'[Date],-1,DAY))
RETURN DIVIDE((Current_Engagement - Previous_Engagement),Previous_Engagement,0) * 100
```
### Total songs
``` Total_songs =
DISTINCTCOUNT('Song Analysis'[Video_id])
```
### Isoutlier
``` IsOutlier = 
IF(ABS([ZScoreEngagementRate]) > 3, 1, 0)
```
### Correlation
This is can be done by using the calculation embbeded in the quick measure option.

### Calculated columns
- Engagement
- Time of day category
- Duration category
- Quarter

## The Analysis
1- Exploratory Data Analysis (EDA):
- Explore patterns and distributions in view counts, like counts, and comments.
- Identify trends in the popularity and engagement of YouTube song videos.

- Identify popular tags and their correlation with view counts.

2- Temporal Trends:
- Explore how YouTube song video metrics vary over time.
- Identify peak publishing times and their impact on engagement

3- User Engagement Insights:
- Investigate relationships between likes, comments, and views.
- Identify factors influencing user engagement with YouTube song videos.

## Insights

### Highest Engagement and Viewer Interaction
- De De Pyaar De had the highest engagement rate of 0.46. 45 engagement actions (likes and comments) per every 100 views. This indicates that a significant portion of the viewers interacted with the song.
- The Song Teaser: Sexy Baby Girl had the lowest engagement rate 0.0, indicating minimal viewer interaction likely due to lack of appeal or interest.
- The highest number of songs published was 4,079 in 2011, accounting for 21.89% of the total songs, 17.86% more than the two least prolific years.
Engagement rates fluctuate over the years, with the highest rate at 1.76 in 2010, dropping to 1.48 as the number of views increased over time.

### Popularity and Engagement Trends
- 2018 recorded the highest number of views, with approximately 32 billion views indicating a surge in user interest or effective marketing.
- 2019 had the highest number of engagements, with about 260,000 likes and comments reflecting active viewer participation.
- There have been inconsistencies in the growth rate of views and engagements over the years. Notably, 2015 experienced a significant growth rate with increases of 0.49 in views and 
  0.28 in engagement from the previous year. However, subsequent years saw fluctuating growth rates in views, likes, and comments possibly due to varying content quality and audience 
  preferences.
- Vaaste Song: This song video had the highest number of likes and comments, making it the most engaged YouTube song video.
- 2018 had the highest average number of views per video, reaching an average of 25,708,792.47 views, a 99.70% increase from the previous year and more than double the average views 
  in 2023. High-definition videos averaged 25,809,479.74 views.
- In 2019, T-Series experienced the highest average number of likes per video, reaching 185,754.51 likes, influenced by high-definition and short-duration videos. All users engaged 
  with HD videos, while the majority liked short-duration videos.

### Channel Insights
- T-Series: The channel had about 19,000 YouTube song videos published, amassing 230 billion views, likes, and comments.

### Popular Tags and Publishing Times
- "Songs" is the most frequently used tag, appearing 16,784 times. However, it has a very low correlation (0.02) with view counts, indicating a slight to no increase in views with 
   the frequency of this tag suggesting tags alone don't drive views.
- The peak times for publishing are in the Morning, Afternoon, and Mid-day (6 AM - 4 PM). The morning has the highest number of songs published (7,157), while night-time has the 
  least (495) possibly due to release strategy and industry practices.
- User engagement with YouTube songs is highest in the morning at 0.81% possibly due to higher viewer availability.

### Relationship between video metrics and Engagement Factors
- The average number of comments per year is 2,673.18.
- Long-duration YouTube song videos receive the most user engagement likely because Informative and educational content can keep viewers engaged for longer periods and encourage them 
  to share their insights or ask questions.
- There is a significant correlation (0.96) between the number of views and likes, indicating that higher views tend to result in higher likes. Similarly, there is a strong 
  correlation (0.85) between views and comments.
- Users prefer high-definition (HD) videos over standard definition, indicating a higher engagement with HD videos.
- There is also a significant correlation (0.86) between likes and comments, suggesting that higher likes tend to result in higher comments and vice versa.
  Weekend Engagement: Engagement rates are higher during weekends, particularly on Sundays, with the highest engagement rate at 0.91% possibly due to more leisure time.
- Morning Releases: Songs released in the morning receive 0.81% engagement, which is 58.82% more than songs released at night, the least popular publishing time likely due to 
  increased daytime activity like listening to songs during commutes.

## Recommendations
1- Stakeholders and content creators should ensure videos released are in high-definition (HD) as they attract more engagement.

2- Focusing on releasing song videos or content in the early hours (morning),to capitalize on higher viewer engagement and minimize night-time releases, as they have the least 
   engagement.
   
3- Ensure videos are in HD, as they attract more engagement. Viewers show a clear preference for better quality.

4- Since long-duration videos drive higher engagement, aim for impactful content that retains viewer attention.

5- Creators should use a mix of trending and relevant tags together with captivating captions to increase discoverability without over-relying on generic tags like "Songs".

6- Stakeholders should plan major releases for weekends to benefit from higher engagement rates.

7- Create content that encourages community interaction, such as Q&A sessions, live streams, and comment shout-outs this way the engagement rate can be increased.

## Limitation
I replaced null values from the description column with N/A 'not available' to ensure the consistency of the data. I also removed Cheez Badi launch event video in my visualization because it is an outlier.

## Reference
[T-Series YouTube](https://medium.com/r/?url=https%3A%2F%2Fwww.youtube.com%2Fchannel%2FUCq-Fj5jknLsUf-MWSy4_brA)




