# Google Data Analytics Capstone: Complete a Case Study

For this case study, I have assumed the role of a junior data analyst working at Cyclistic, a bike-share company in Chicago. The company believes that future success depends on maximizing the number of annual memberships. I will be using the 6 phases of the data analytics process: Ask, Prepare, Process, Analyze, Share, and Act.

This case study is delivered from Google through their [Coursera course](https://www.coursera.org/programs/career-academy-alumni-yzapn/professional-certificates/google-data-analytics).

## Ask

### What is the business task?

I will be working to discover how annual members and casual riders differ in their usage of Cyclistic bikes. The problem I am solving is discovering how to maxmize annual memberships by converting casual riders.

### How can my insights drive business decisions?

By analyzing the data and drawing conclusions, the business can better understand their clients and target their marketing to increase annual memberships.

### The key stakeholders

1. The Director of Marketing
2. The Marketing Analytics team
3. The Cyclistic executive team

## Prepare

### Data

I will be drawing my insights from a twelve month period ranging from April of 2022 to March of 2023. The datasets can be accessed [here](https://divvy-tripdata.s3.amazonaws.com/index.html).

This data is organized per month into CSV files with a naming convention of YYYYMM-divvy-tripdata and is a secondary source collected by Divvy. It is made public by this [license agreement](https://ride.divvybikes.com/data-license-agreement). The data contains information for:

- Trip start date and time
- Trip end date and time
- Trip start station
- Trip end station
- Rider type (i.e. member, single ride, or day pass)

## Process

The tools I will be using in this case study are HeidiSQL, and Tableau. I have chosen these tools because of a familiarity with MySQL and Tableau for its versatility with visualization.

To begin the analysis, I imported all the CSV files into a database named 'cyclistic_case_study' that was created in HeidiSQL. Each CSV file was imported into its own table within the database, where I normalized the column names and data types.

### Cleaning

I first take steps to ensure there are no duplicate values. Using the ride_id column as the primary key, I created queries that counted this column and compared the value to a similar query that selected the distinct values from the same column.

<img width="278" alt="distinct_values" src="https://github.com/Herringtonjc/cyclistic-case-study/assets/7733046/534b6021-93f0-4d19-b4a6-7db947881e4e">

Secondly, I checked for rows that were missing information in 'start_station_name', 'end_station_name', start_station_id', or 'end_station_id'. I removed 1,030,289 rows of data where these values were missing.

<img width="188" alt="clean_missing_data" src="https://github.com/Herringtonjc/cyclistic-case-study/assets/7733046/4a09e201-ea9a-4a26-86c4-0d06ec17e611">

Upon further checking of the data, I noticed the 'started_at' and 'ended_at' columns for my '202204_divvy_tripdata' table were not in a DATETIME format. The other tables in my database have these columns in a YYYY-MM-DD format, whereas the table in question is using a string value of M/D/YYYY.

I used the STR_TO_DATE() function in MySQL to convert these strings into a datetime format. Some of the tables had a column name 'member_casual', while still others had the column name 'member_casual' before importing all the data from the twelve tables into a single, normalized table named 'tripdata_combined'.

## Analyze

The data was organized into one table to be easier to query after all null or empty values were removed. The 'ride_id' column served as the primary key to check for duplicity, the count of the 'ride_id' was used to determine popular times and locations for rentals which required the use of the start times and the start locations. I also compared the amount of members versus casual riders. It was surprising to find that almost half of all riders were already annual members.

![casual-vs-member](https://github.com/Herringtonjc/cyclistic-case-study/assets/7733046/e2356b2a-40c2-4a43-b4ba-45bc2b9c3743)

These insights can be useful in determining which stations and during which times targeted advertising would be the most effective.

## Share

During analysis, I discovered that riders tend to prefer renting bycicles during the warmer months and rentals sharply drop off during colder months of the year. Furthermore, I discovered that some rental stations were more popular than others, with some stations having as little as one rental.

![riders-per-month](https://github.com/Herringtonjc/cyclistic-case-study/assets/7733046/0121a4b7-3273-491d-a6cf-4ebd811909cf)

![popular-locations](https://github.com/Herringtonjc/cyclistic-case-study/assets/7733046/b2c95b97-438c-418c-8879-aa2ceb0c932a)

These insights were developed based on the necessity of converting already paying casual members into annual subscription members.

The audience of this presentation is intended to be the marketing department. It is my opinion that the visualizations included with this report will be useful in determining the hotspots for advertising and marketing.

Further analysis could be done to indicate the number of annual members versus casual riders at each location to further direct marketing to casual members.

## Act

The final conclusion is that with proper advertising at the more popular stations and during the busier months will convert more casual riders to an annual membership.
