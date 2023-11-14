# Hoterevenue-
 #HotelBookingData
Hotel Booking Data 
Requirements Questions

1. Is our hotel revenue growing by year?
   - We have two hotel types so it would be good to segment revenue by hotel type
2. Should we increase our parking lot size?
   - We want to understand if there is a trend in guests with personal cars
3. What trends can we see in the data?
   - Focus on average daily rate and guests to explore seasonality
  
  I Create a database ( SQL Server Management Studio)
   Querying data
   Exploratory Data Analysis
   Create Data Visualizations using Power BI

   II Querying the Data
A. Fetching Data from Tables
To fetch data to view from the tables, we will use the following command. The wildcard ‘*’ operator is used to retrieve all the data from the table.
select * from dbo.['2018$']
select * from dbo.['2019$']
select * from dbo.['2020$']

B.Combining the Data
To combine the data from the three tables, we simply use the UNION operator among these commands.
select * from dbo.['2018$']
union
select * from dbo.['2019$']
union
select * from dbo.['2020$']

III Exploratory Data Analysis (EDA)
Now, we are going to apply EDA to the data and try to answer the following questions.

Is our hotel revenue growing yearly?
Should we increase our parking lot size?
What trends can we see in the data?
code: with hotels as(
select * from dbo.['2018$']
union
select * from dbo.['2019$']
union
select * from dbo.['2020$'])

select * from hotels

Q.1: Is our hotel revenue growing yearly?
select 
  (stays_in_week_nights + stays_in_weekend_nights) * adr
  as revenue from hotels
  select 
arrival_date_year
sum((stays_in_week_nights + stays_in_weekend_nights) * adr)
as revenue from hotels group by arrival_date_year

Also, determine the revenue trend by hotel type by grouping the data by hotel and then seeing which hotels have generated the most revenue.

select 
arrival_date_year, hotel,
sum((stays_in_week_nights + stays_in_weekend_nights) * adr)
as revenue from hotels group by arrival_date_year, hotel
Q.2: Should we increase our parking lot size?
To answer this question, we will focus on the car_parking_spaces and the number of guests staying in the hotel. So, let’s do it by applying the following SQL query.

select
arrival_date_year, hotel,
sum((stays_in_week_nights + stays_in_weekend _nights) * adr) as revenue,
concat (round((sum(required_car_parking_spaces)/sum(stays_in_week_nights +
stays_in_weekend_nights)) * 100, 2), '%') as parking_percentage
from hotels group by arrival_date_year, hotel

IV: Create Data Visualizations Using Power BI
First Left Join: Combines the hotels table with the market_segment table by matching the market_segment column in the “hotels” table with the market_segment.market_segment column.

Second Left Join: Combines the hotel table with the meal_cost table by matching the meal column in the hotel table and the meal_cost.meal column.

with hotels as(
select * from dbo.['2018$']
union
select * from dbo.['2019$']
union
select * from dbo.['2020$'])

select * from hotels
left join dbo.market_segment$
on hotels.market_segment = market_segment$.market_segment
left join dbo.meal_cost$
on meal_cost$.meal = hotels.meal

Conclusions
Q.3: What trends can we see in the data?
- Revenue increased from 2018 to 2019, but it began to decrease from 2019 to 2020.
- The average daily rate (ADR) has increased from 2019 to 2020, from $99.53 to $104.47.
- The total number of nights booked by customers decreased from 2019 to 2020.
- The discount percentage offered by the hotel has increased from 2019 to 2020 to attract more customers.

