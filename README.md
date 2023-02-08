# Cyclistic-Case-Study
This is a case study for a bike share company, Cyclistic, where we analyze historical bike trip data to identify trends and gain insights into the behavior and preferences of casual riders in order to inform the development of effective marketing strategies aimed at converting them into annual members. 

## **Introduction**

Cyclistic is a bike-share company located in Chicago looking to maximize on the number of annual subscribers. After launching in 2016, the company has grown rapidly to a fleet of 5,824 bicycles that are geotracked and locked into a network of 692 stations across Chicago. The bikes can be unlocked from one station and returned to any other station in the system anytime. 

Cyclistic’s previous marketing strategy focused on building general awareness and appealing to a wide range of consumers. They achieved this through flexible pricing options such as single-ride passes, full-ride passes and annual memberships. Customers who purchase single-ride or full-day passes are referred to as “casual riders”, while those who purchase annual memberships are called “Cyclistic members”.

The company’s finance analysts have determined that annual members are more profitable than casual riders. The director of marketing, Moreno, believes that increasing the number of annual members is crucial for future growth. Instead of targeting all new customers, Moreno plans to focus on converting casual riders into members. This is because casual riders are already familiar with the Cyclistic program and have chosen it for their transportation needs. This strategy should help maximize profitability and drive growth for the company.

Moreno’s goal is to design marketing strategies that will convert casual riders in to annual members. To achieve this, the marketing team must first gain a deeper understanding of the differences between annual members and casual riders, as well as the reasons why casual riders would consider purchasing a membership. Additionally, they want to explore how digital media could impact their marketing tactics. To gain this understanding, Moreno and her team plan to analyze historical data to identify trends. This data will provide valuable insights into the behavior and preferences of casual riders, which will inform the development of effective conversion strategies.

## **Business Task**

Analyze historical bike trip data to identify trends and gain insights into the behavior and preferences of casual riders in order to inform the development of effective marketing strategies aimed at converting them into annual members. 

## **Objectives**

- Increase number of annual members in order to drive future growth for the company.
- Understand the differences between annual members and casual riders and the reasons why casual riders would consider buying a membership.
- Analyze historical bike trip data to identify trends and gain insights into behavior and preferences of casual riders to help inform development of effective marketing strategies aimed at converting them into annual members.

## **Key Stakeholders**

1. **Cyclistic:** A bike-share program that features more than 5,800 bicycles and 600 docking stations.  The program offers reclining bikes, hand tricycles and cargo bikes, making it more inclusive to people with disabilities and riders who can’t use standard two-wheeled bikes. Majority of the riders opt for traditional bikes, about 8% use the assistive options. Cyclistic users are more likely to ride for leisure, but about 30% use them to commute to work each day.
2. **Lily Moreno:** The director of marketing. Moreno is responsible for the development of campaigns and initiatives to promote the bike-share program. These may include email, social media, and other channels.
3. **Cyclistic marketing analytics team:** A team of data analysts who are responsible for collecting, analyzing and reporting data that helps guide Cyclistic marketing strategy.
4. **Cyclistic executive team:** The notoriously detail-oriented executive team will decide whether to approve the recommended marketing program.

## **Scope of the study**

The study will involve analysis of historical data of the bike-share program to identify trends and gain insights into preferences of casual riders.

## **Methodology**

Follow Google Analytics methodology in analyzing datasets. The phases of data analysis followed are as follows:
1. Ask
2. Prepare
3. Process
4. Analysis
5. Share
6. Act

## **Ask**

The questions that need to be answered are:
1. How do annual members and casual riders use Cyclistic bikes differently?
2. Why would casual riders buy Cyclistic annual memberships?
3. How can Cyclistic use digital media to influence casual riders to become members?

## **Prepare**

The data is structured, organized in rows (records) and columns (fields). Each record represents one trip and each trip has a unique field that identifies it, ride_id. Each trip is anonymized and includes the following fields:
- ride_id- Ride id – unique
- rideable_type- Bike type - Classic, Docked, Electric
- started_at- Trip start day and time
- ended_at- Trip end day and time
- start_station_name- Trip start station
- start_station_id- Trip start station id
- end_station_name- Trip end station
- end_station_id- Trip end station id
- start_lat- Trip start latitude
- start_lng- Trip start longitude
- end_lat- Trip end latitude
- end_lat- Trip end longitude
- member_casual- Rider type - Member or Casual  

The dataset follows ROCCC:
- Reliable- The data is reliable, not biased.
- Original- The original data set can be located publicly.
- Comprehensive- There is no important data that is missing data.
- Current- The dataset is updated monthly, hence current.
- Cited- The dataset is cited.

The dataset is made publicly available on this [link](https://divvy-tripdata.s3.amazonaws.com/index.html) here by Motivate International Inc. under this [license](https://ride.divvybikes.com/data-license-agreement.)

Key tasks followed:
1. I downloaded the data and stored copies in the computer.
2. The downloaded data was monthly data for the last 14 months, from December 2021 to January 2023.
3. The data is stored in CSV (comma-separated values) format and there is a total of 13 columns.
4. I uploaded the data into a database, Cyclistic Case Study, in Microsoft SQL Server Management Studio

## **Process**

This step is to ensure that the data is stored appropriately and prepared for analysis. I stored the files in a folder in the desktop for upload to Microsoft SQL Server Studio Management.

### **Microsoft Excel: Initial data cleaning and manipulation**

Here I did the following for all the 12 CSV files:
- Separated the started_at column data into start_date and start_time columns
    - Used this function =DATE(YEAR(C2), MONTH(C2), DAY(C2)) for the start_date column and =TIME(HOUR(C2), MINUTE(C2), SECOND(C2)) for the start_time column
    - Formatted the start_date column in YYYY-MM-DD format and start_time column in HH: MM: SS format
- Separated the ended_at column data into end_date and end_time columns
    - Used this function =DATE(YEAR(C2), MONTH(C2), DAY(C2)) for the end_date column and =TIME(HOUR(C2), MINUTE(C2), SECOND(C2)) for the end_time column
    - Formatted the end_date column in YYYY-MM-DD format and end_time column in HH: MM: SS format\

### **SQL Server Management Studio**

Here I uploaded all the monthly Excel worksheet files into SQL Server Management to database named CyclisticCaseStudy. I took the following steps to clean the data:

- Merged all monthly files into one using UNION function to create the full fiscal year table called CyclisticFullYear
            
            SELECT [ride_id],[rideable_type],[start_date],[start_time],[end_date],[end_time],
            [start_station_name],[start_station_id],[end_station_name],[end_station_id],[start_lat],[start_lng],
            [end_lat],[end_lng],[member_type] INTO CyclisticFullYear FROM CyclisticCaseStudy..Jan2022
            UNION
            SELECT [ride_id],[rideable_type],[start_date],[start_time],[end_date],[end_time],
            [start_station_name],[start_station_id],[end_station_name],[end_station_id],[start_lat],[start_lng],
            [end_lat],[end_lng],[member_type] FROM CyclisticCaseStudy..Feb2022
            UNION
            SELECT [ride_id],[rideable_type],[start_date],[start_time],[end_date],[end_time],
            [start_station_name],[start_station_id],[end_station_name],[end_station_id],[start_lat],[start_lng],
            [end_lat],[end_lng],[member_type] FROM CyclisticCaseStudy..Mar2022
            UNION
            SELECT [ride_id],[rideable_type],[start_date],[start_time],[end_date],[end_time],
            [start_station_name],[start_station_id],[end_station_name],[end_station_id],[start_lat],[start_lng],
            [end_lat],[end_lng],[member_type] FROM CyclisticCaseStudy..April2022
            UNION
            SELECT [ride_id],[rideable_type],[start_date],[start_time],[end_date],[end_time],
            [start_station_name],[start_station_id],[end_station_name],[end_station_id],[start_lat],[start_lng],
            [end_lat],[end_lng],[member_type] FROM CyclisticCaseStudy..May2022
            UNION
            SELECT [ride_id],[rideable_type],[start_date],[start_time],[end_date],[end_time],
            [start_station_name],[start_station_id],[end_station_name],[end_station_id],[start_lat],[start_lng],
            [end_lat],[end_lng],[member_type] FROM CyclisticCaseStudy..June2022
            UNION
            SELECT [ride_id],[rideable_type],[start_date],[start_time],[end_date],[end_time],
            [start_station_name],[start_station_id],[end_station_name],[end_station_id],[start_lat],[start_lng],
            [end_lat],[end_lng],[member_type] FROM CyclisticCaseStudy..Jul2022
            UNION
            SELECT [ride_id],[rideable_type],[start_date],[start_time],[end_date],[end_time],
            [start_station_name],[start_station_id],[end_station_name],[end_station_id],[start_lat],[start_lng],
            [end_lat],[end_lng],[member_type] FROM CyclisticCaseStudy..Aug2022
            UNION
            SELECT [ride_id],[rideable_type],[start_date],[start_time],[end_date],[end_time],
            [start_station_name],[start_station_id],[end_station_name],[end_station_id],[start_lat],[start_lng],
            [end_lat],[end_lng],[member_type] FROM CyclisticCaseStudy..Sep2022
            UNION
            SELECT [ride_id],[rideable_type],[start_date],[start_time],[end_date],[end_time],
            [start_station_name],[start_station_id],[end_station_name],[end_station_id],[start_lat],[start_lng],
            [end_lat],[end_lng],[member_type] FROM CyclisticCaseStudy..Oct2022
            UNION
            SELECT [ride_id],[rideable_type],[start_date],[start_time],[end_date],[end_time],
            [start_station_name],[start_station_id],[end_station_name],[end_station_id],[start_lat],[start_lng],
            [end_lat],[end_lng],[member_type] FROM CyclisticCaseStudy..Nov2022
            UNION
            SELECT [ride_id],[rideable_type],[start_date],[start_time],[end_date],[end_time],
            [start_station_name],[start_station_id],[end_station_name],[end_station_id],[start_lat],[start_lng],
            [end_lat],[end_lng],[member_type] FROM CyclisticCaseStudy..Dec2022;
         
- Cleaned NULL VALUES in start_station_name, start_station_id, end_station_name and end_station_id columns- I merged NULL station_ids with their respective values from rows above that had the corresponding station_ids

            UPDATE CyclisticFullYear
            SET start_station_id = (
                SELECT start_station_id
                FROM (
                    SELECT [start_station_name], [start_station_id], ROW_NUMBER() OVER (PARTITION BY [start_station_name] ORDER BY [start_station_id]) as row_num
                    FROM CyclisticFullYear
                    WHERE [start_station_id] IS NOT NULL
                ) t
                WHERE t.[start_station_name] = CyclisticFullYear.[start_station_name] AND t.row_num = 1
            )
            WHERE [start_station_id] IS NULL;


            UPDATE CyclisticFullYear
            SET end_station_id = (
                SELECT end_station_id
                FROM (
                    SELECT [end_station_name], [end_station_id], ROW_NUMBER() OVER (PARTITION BY [end_station_name] ORDER BY [end_station_id]) as row_num
                    FROM CyclisticFullYear
                    WHERE [end_station_id] IS NOT NULL
                ) t
                WHERE t.[end_station_name] = CyclisticFullYear.[end_station_name] AND t.row_num = 1
            )
            WHERE [end_station_id] IS NULL;

- Removed NULL and duplicate row id

    - Counted duplicate row ids- 9 duplicates
            
            SELECT COUNT(*)
            FROM master.. CyclisticFullYear
            GROUP BY ride_id
            HAVING COUNT(*) > 1
            
    - Delete duplicates

            WITH CTE AS (
              SELECT [ride_id], ROW_NUMBER() OVER (PARTITION BY [ride_id] ORDER BY [ride_id]) as row_num
              FROM master.. CyclisticFullYear
            )
            DELETE FROM CTE WHERE row_num > 1 

            SELECT COUNT(DISTINCT [ride_id])  FROM master..CyclisticFullYear

- Checked and deleted NULLS
            
            SELECT COUNT(*)
            FROM master.. CyclisticFullYear
            WHERE ride_id IS NULL  ---1 NULL Value

            DELETE FROM master.. CyclisticFullYear
            WHERE ride_id IS NULL;  ---1 row is deleted

- Checked for NULLS in start_date, start_time, end_date, end_time

            SELECT COUNT(*)
            FROM master.. CyclisticFullYear
            WHERE end_date IS NULL ---1 value

- Checked for spelling errors in rideable_type and member_type columns

            ----rideable_type column- 0 spelling errors
            SELECT rideable_type 
            FROM master.. CyclisticFullYear	
            WHERE rideable_type NOT LIKE '%electric_bike%' 
            AND rideable_type NOT LIKE '%docked_bike%' 
            AND rideable_type NOT LIKE '%classic_bike%' 

            ----member_type column- 0 spelling errors
            SELECT member_type 
            FROM master.. CyclisticFullYear 
            WHERE member_type NOT LIKE '%casual%' 
            AND member_type NOT LIKE '%member%'

- I deleted the start_station_name, start_station_id, end_station_name and end_station_id columns because they had a lot of NULLS

            ALTER TABLE CyclisticFullYear
            DROP COLUMN start_station_name, start_station_id, end_station_name, end_station_id

- Created start_datetime and end_datetime columns

            -- Add a new column called "start_datetime" to the "FFF5" table
            ALTER TABLE CyclisticFullYear
            ADD start_datetime DATETIME;

            -- Update the new column with the combined start_datetime values
            UPDATE CyclisticFullYear
            SET start_datetime = CONVERT(DATETIME,CONVERT(VARCHAR(10), start_date, 120) + ' ' + CONVERT(VARCHAR(8), start_time, 108))

            -- Add a new column called "end_datetime" to the "FFF5" table
            ALTER TABLE CyclisticFullYear ADD end_datetime DATETIME;

            -- Update the new column with the combined end_datetime values
            UPDATE CyclisticFullYear
            SET end_datetime = CONVERT(DATETIME,CONVERT(VARCHAR(10), end_date, 120) + ' ' + CONVERT(VARCHAR(8), end_time, 108))


            -- Drop start_date, start_time, end_date, end_time columns
            ALTER TABLE CyclisticFullYear
            DROP COLUMN start_date, start_time, end_date, end_time

- I dropped start_date, start_time, end-date and end_time columns
            
            -- Drop start_date, start_time, end_date, end_time columns
            ALTER TABLE CyclisticFullYear
            DROP COLUMN start_date, start_time, end_date, end_time

- I then exported the monthly data to Excel files, which I will do further cleaning in Python- Ran the code below and copied the results into Excel files.

            --Jan
            SELECT *
            FROM CyclisticFullYear
            WHERE start_datetime BETWEEN '2022-01-01 00:00:00' AND '2022-01-31 23:59:59'
            ORDER BY start_datetime;

            --Feb
            SELECT *
            FROM CyclisticFullYear
            WHERE start_datetime BETWEEN '2022-02-01 00:00:00' AND '2022-02-28 23:59:59'
            ORDER BY start_datetime;

            --March
            SELECT *
            FROM CyclisticFullYear
            WHERE start_datetime BETWEEN '2022-03-01 00:00:00' AND '2022-03-31 23:59:59'
            ORDER BY start_datetime;

            --April
            SELECT *
            FROM CyclisticFullYear
            WHERE start_datetime BETWEEN '2022-04-01 00:00:00' AND '2022-04-30 23:59:59'
            ORDER BY start_datetime;

            --May
            SELECT *
            FROM CyclisticFullYear
            WHERE start_datetime BETWEEN '2022-05-01 00:00:00' AND '2022-05-31 23:59:59'
            ORDER BY start_datetime;

            --June
            SELECT *
            FROM CyclisticFullYear
            WHERE start_datetime BETWEEN '2022-06-01 00:00:00' AND '2022-06-30 23:59:59'
            ORDER BY start_datetime;

            --July
            SELECT *
            FROM CyclisticFullYear
            WHERE start_datetime BETWEEN '2022-07-01 00:00:00' AND '2022-07-31 23:59:59'
            ORDER BY start_datetime;

            --August
            SELECT *
            FROM CyclisticFullYear
            WHERE start_datetime BETWEEN '2022-08-01 00:00:00' AND '2022-08-31 23:59:59'
            ORDER BY start_datetime;

            --September
            SELECT *
            FROM CyclisticFullYear
            WHERE start_datetime BETWEEN '2022-09-01 00:00:00' AND '2022-09-30 23:59:59'
            ORDER BY start_datetime;

            --October
            SELECT *
            FROM CyclisticFullYear
            WHERE start_datetime BETWEEN '2022-10-01 00:00:00' AND '2022-10-31 23:59:59'
            ORDER BY start_datetime;

            --November
            SELECT *
            FROM CyclisticFullYear
            WHERE start_datetime BETWEEN '2022-11-01 00:00:00' AND '2022-11-30 23:59:59'
            ORDER BY start_datetime;

            --December
            SELECT *
            FROM CyclisticFullYear
            WHERE start_datetime BETWEEN '2022-12-01 00:00:00' AND '2022-12-31 23:59:59'
            ORDER BY start_datetime;

### **Python**

I then uploaded the Excel files to Jupyter Notebook for further cleaning and analysis. 
The following were the cleaning steps taken:

- Merged all the datasets into one dataframe called Cyclistic_data
- Checked the data types of all columns and changed rideable_type and member_type columns into categorical datatype.
- Dropped the start_lat, start_lng_ end_lat, end_lng columns because they had a lot of NULLS.
- Created a new column, ride_length, in HH: MM: SS format by subtracting start_date time from the end_datetime column.
- Checked and dropped ride_lengths that were negative, end_datetime < start_datetime, or below 60 seconds.
- Created a new column, day_of_week, by extracting the day of the week from the start_datetime column.
- Changed the day_of_week datatype into categorical datatype.
- Created new column, month_name and month, by extracting the month name and number from the start_datetime column.
- Changed the month_name datatype into categorical datatype.

The next steps in Python are contained in the Complete Cyclistic Case Study.ipynp file attached in this repository.

 
 
 
 
 
 
 
 
 
 
