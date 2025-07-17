# Google Data Analytics Capstone Project
### Case study: How does a bike-share navigate speedy success?

# 1. Introduction
 This Case Study is to demonstrate the skills I learned in the Google Data Analytics Course. In this program, I learned how to clean and organize
 data for analysis, and complete analysis and calculations using spreadsheets, SQL and R programming. I also learned how to visualize and 
 present data findings in dashboards, and in presentations using Tableu.

In this Case Study, I will comlepete an analysis for a ficticious bike-share program named Cyclistic along with some key team members, using 
SQL to clean, organize, analyze, and calulate. I will aslo be using Tableu to create diagrams to share my findings and present my complete analysis.

# 2. Scenario

I am a junior data analyst working on the marketing analyst team at Cyclistic, a bike-share
company in Chicago. The director of marketing believes the company’s future success
depends on maximizing the number of annual memberships. Therefore, the team wants to
understand how casual riders and annual members use Cyclistic bikes dierently. From these
insights, the team will design a new marketing strategy to convert casual riders into annual
members. But first, Cyclistic executives must approve our recommendations, so they must be
backed up with compelling data insights and professional data visualizations.

### Characters & Teams

* **Cyclistic**   
A bike-share program that features more than 5,800 bicycles and 600
docking stations. Cyclistic sets itself apart by also offering reclining bikes, hand
tricycles, and cargo bikes, making bike-share more inclusive to people with disabilities
and riders who can’t use a standard two-wheeled bike. The majority of riders opt for
traditional bikes; about 8% of riders use the assistive options. Cyclistic users are more
likely to ride for leisure, but about 30% use the bikes to commute to work each day.
* **Lily Moreno**   
The director of marketing and our manager. Moreno is responsible for
the development of campaigns and initiatives to promote the bike-share program.
These may include email, social media, and other channels.
* **Cyclistic Marketing Analytics Team**   
A team of data analysts who are responsible for
collecting, analyzing, and reporting data that helps guide Cyclistic marketing strategy.
I joined this team six months ago and have been busy learning about Cyclistic’s
mission and business goals, as well as how I can help Cyclistic achieve them.
* **Cyclistic Executive Team**   
The notoriously detail-oriented executive team will decide
whether to approve the recommended marketing program.

### About the Company

In 2016, Cyclistic launched a successful bike-share offering. Since then, the program has grown
to a fleet of 5,824 bicycles that are geotracked and locked into a network of 692 stations across
Chicago. The bikes can be unlocked from one station and returned to any other station in the
system anytime.

Until now, Cyclistic’s marketing strategy relied on building general awareness and appealing to
broad consumer segments. One approach that helped make these things possible was the
flexibility of its pricing plans: single-ride passes, full-day passes, and annual memberships.
Customers who purchase single-ride or full-day passes are referred to as casual riders.
Customers who purchase annual memberships are Cyclistic members.

Cyclistic’s finance analysts have concluded that annual members are much more profitable
than casual riders. Although the pricing flexibility helps Cyclistic attract more customers,
Moreno believes that maximizing the number of annual members will be key to future growth.
Rather than creating a marketing campaign that targets all-new customers, Moreno believes
there is a solid opportunity to convert casual riders into members. She notes that casual riders
are already aware of the Cyclistic program and have chosen Cyclistic for their mobility needs.

Moreno has set a clear goal: Design marketing strategies aimed at converting casual riders into
annual members. In order to do that, however, the team needs to beer understand how
annual members and casual riders differ, why casual riders would buy a membership, and how
digital media could affect their marketing tactics. Moreno and her team are interested in
analyzing the Cyclistic historical bike trip data to identify trends.

# 3. Data Analysis Process
In this Case Study, I will be using a 6 step analysis process to solve the problem.
Those steps are as follows:
1. Ask
2. Prepare
3. Process
4. Analyze
5. Share
6. Act

## **Step One: Ask**
The Cyclistic Marketing Analytics Team came up with three questions that will guide the future marketing program:
1. How do annual members and casual riders use Cyclistic bikes dierently?
2. Why would casual riders buy Cyclistic annual memberships?
3. How can Cyclistic use digital media to influence casual riders to become members?

Moreno has assigned me the first question to answer: How do annual members and casual
riders use Cyclistic bikes differently?

## **Step Two: Prepare**
**Data Source**   
Because Cyclistic is a fictitional company, I will be using the January 2024 - December 2024 data from [The City of Chicago’s Divvy bicycle sharing service](https://divvy-tripdata.s3.amazonaws.com/index.html)
to analyze and identify current trends in riders behavior. The data has been made available by Motivate International Inc. under this [license](https://divvybikes.com/data-license-agreement).

**Data Organization**  
The data is organized by month, and follows the naming covention of *"YYYYMM-divvy-tripdata"*. Each dataset includes all of the trips
that were completed in the month, and contains the following data column names:   
* ride_id
* rideable_type
* started_at
* ended_at
* start_station_name
* start_station_id
* end_station_name
* end_station_id
* start_lat
* start_lng
* end_lat
* end_lng
* member_casual

**ROCCC**  
ROCCC is an acronym that is used to help determine weither a dataset is biased. It stands for  

R- Reliable  
O- Original  
C- Comprehensive  
C- Current  
C- Cited  

The dataset comes directly from Divvy's parent company Lyft Bikes and Scooters LLC, so I can be sure that the data is reliable, original, and cited.
There are 13 columns of data for each trip so the data is comprehensive, and the datasets are from the past year making them current.  

## **Step Three: Process**  
For this study, I am using Google's BigQuery to complete my analysis.  
  
**Data Combining**  
I've combined the 12 datasets into one dataset I named *"combined_2024_tripdata"* to easily clean and analyze the data. I used the following
code to generate the new table:
```
CREATE TABLE IF NOT EXISTS `cyclistic-466120.combined_2024_tripdata.combined_2024_tripdata` AS 
(
  SELECT * FROM `monthly_2024_tripdata.202401-divvy-tripdata`
  UNION ALL
  SELECT * FROM `monthly_2024_tripdata.202402-divvy-tripdata`
  UNION ALL
  SELECT * FROM `monthly_2024_tripdata.202403-divvy-tripdata`
  UNION ALL
  SELECT * FROM `monthly_2024_tripdata.202404-divvy-tripdata`
  UNION ALL
  SELECT * FROM `monthly_2024_tripdata.202405-divvy-tripdata`
  UNION ALL
  SELECT * FROM `monthly_2024_tripdata.202406-divvy-tripdata`
  UNION ALL
  SELECT * FROM `monthly_2024_tripdata.202407-divvy-tripdata`
  UNION ALL
  SELECT * FROM `monthly_2024_tripdata.202408-divvy-tripdata`
  UNION ALL
  SELECT * FROM `monthly_2024_tripdata.202409-divvy-tripdata`
  UNION ALL
  SELECT * FROM `monthly_2024_tripdata.202410-divvy-tripdata`
  UNION ALL
  SELECT * FROM `monthly_2024_tripdata.202411-divvy-tripdata`
  UNION ALL
  SELECT * FROM `monthly_2024_tripdata.202412-divvy-tripdata`
);
```
Then I perform the following query to find that we are starting with 5,860,568 rows of data for the entire year.

```
SELECT count(*) as total_records 
FROM `cyclistic-466120.combined_2024_tripdata.combined_2024_tripdata`;
```

**Data Cleaning**  
Before we can clean the data I will make a duplicate table named "cleaned_2024_tripdata" so in case I make any irreversable errors, I have a data set that I can return 
to. Now we must ensure that the data is clean, concistant, and does not contain any errors. First I will check the metadata to see if there are any 
inconsistencies.  

```
SELECT column_name, data_type
FROM combined_2024_tripdata.INFORMATION_SCHEMA.COLUMNS
WHERE table_name = 'cleaned_2024_tripdata';
```

After checking, I have found no inconsistencies and have identified the ride_id column to be the primary key.
Then I will check for any duplicate values and it appears there are none.  

```
SELECT COUNT(ride_id) - COUNT(DISTINCT ride_id) AS duplicate_rows
FROM cyclistic.`all-2024-divvy-tripdata`;
```
a
```

```
------
git rid of nulls

calc trip_duration_minutes, hour, day of: week, month, year

git rid of min <0 and >= 1440 
------
## **Step Four: Analyze**
------
find the ride total, average, maximum and minimum trip duration for different ride types by casual and member riders

find the ride total, average, maximum and minimum trip duration for each month by casual and member riders

find the ride total, average, maximum and minimum trip duration for each day of the week by casual and member riders.

find the ride total, average, maximum and minimum trip duration at each start station by casual and member riders.
------
## **Step Five: Share**

------

------
## **Step Six: Act**
