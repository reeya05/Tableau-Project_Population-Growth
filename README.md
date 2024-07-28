**# Tableau-Project_Population-Growth**
Unveiling Population Dynamics: A Tableau Journey through 2023 and 2024

**## Project Overview**
This project analyzes the world population growth rates for the years 2023 and 2024 using Tableau Desktop version 2024.2.0. It includes data cleaning steps, SQL queries for data extraction and transformation, and various visualizations to present the findings.

**## Data Source**

The data used in this project is sourced from [Kaggle : World population growth rate by cities 2024]((https://www.kaggle.com/datasets/dataanalyst001/world-population-growth-rate-by-cities-2024)). The dataset includes information on the population growth rates of the top 800 populated cities around the world for the years 2023 and 2024.

**## Data Cleaning and Checking Steps**
Before analyzing the dataset, it's crucial to perform data cleaning and checking to ensure data quality. Here are the steps used to clean and check the dataset:

_### 1. Check For Missing Values_
Used MySQL Workbench 8.0 to check for missing values. All columns had zero missing values.
```sql
SELECT
  SUM(CASE WHEN city IS NULL THEN 1 ELSE 0 END) AS missing_city,
  SUM(CASE WHEN country IS NULL THEN 1 ELSE 0 END) AS missing_country,
  SUM(CASE WHEN continent IS NULL THEN 1 ELSE 0 END) AS missing_continent,
  SUM(CASE WHEN population_2023 IS NULL THEN 1 ELSE 0 END) AS missing_population_2023,
  SUM(CASE WHEN population_2024 IS NULL THEN 1 ELSE 0 END) AS missing_population_2024,
  SUM(CASE WHEN growth_rate IS NULL THEN 1 ELSE 0 END) AS missing_growth_rate
FROM sales.`world population growth rate by cities 2024`;

_### 2. Data Cleaning Steps_
Add Missing Values : Used Google Sheets to add any missing values where necessary.
Removing Errors in Field Names: Corrected errors in field names (e.g., changed "Oceana" to "Oceania") using Google Sheets.

_### 3. Data Inspection Using SQL_
-- Initial inspection
SELECT * 
FROM sales.`world population growth rate by cities 2024`
LIMIT 10;

-- Check dataset size
SELECT COUNT(*)
FROM sales.`world population growth rate by cities 2024`;

-- Finding Minimum Growth Rate with City, Country, and Continent
SELECT 
    city,
    country,
    continent,
    growth_rate
FROM 
    sales.`world population growth rate by cities 2024`
WHERE 
    growth_rate = (SELECT MIN(growth_rate) FROM sales.`world population growth rate by cities 2024`);

-- Finding Maximum Growth Rate with City, Country, and Continent
SELECT 
    city,
    country,
    continent,
    growth_rate
FROM 
    sales.`world population growth rate by cities 2024`
WHERE 
    growth_rate = (SELECT MAX(growth_rate) FROM sales.`world population growth rate by cities 2024`);


**## Step-by-Step Guide to Creating a Tableau Dashboard**

**_### 1. Connect to Data_**
- Step 1: Open Tableau and select “Connect.”
- Step 2: Choose your data source (e.g., Excel, CSV, Database).
- Step 3: Navigate to the dataset file and click “Open.”
- Step 4: Verify the data is loaded correctly in the Data Source tab.

**_### 2. Data Preparation_**
- Step 1: Inspect the data in the Data Source tab.
- Step 2: Rename fields for clarity if needed (right-click on column header > Rename).

_**### 3. Tableau Visualizations**_
_1. Population Growth Trends by Continent_
Chart Type: Line Chart

- Drag 'continent' to Columns shelf.
- Drag 'population_2023' and 'population_2024' to Rows shelf.
- Use different line charts for different years.

_2. Top Countries Driving Population Growth_
Chart Type: Treemap

- Drag 'continent' to Columns shelf.
- Drag 'country' to Rows shelf.
- Drag 'growth_rate' to Size/Color.

_3. Top 10 Cities with Highest and Lowest Growth Rates_
Chart Type: Bar Chart

Create 2 worksheets: one for the top 10 highest and another for the top 10 lowest growth rates.

For the highest growth rates:
- Drag 'city' to Rows shelf.
- Drag 'growth_rate' to Columns shelf.
- Sort cities by 'growth_rate' (Descending).
- Filter to the Top 10 by 'growth_rate'.

For the lowest growth rates:
- Create a calculated field 'Negative Growth Rate':
```tableau
-[growth_rate]

Drag 'city' to Rows shelf.
- Drag 'Negative Growth Rate' to Columns shelf.
- Sort cities by 'Negative Growth Rate' (Descending).
- Filter to the Top 10 by 'Negative Growth Rate'.

_4. Correlation Between Population Size and Growth Rate_
Chart Type: Scatter Plot

- Drag 'population_2023' to Columns shelf.
- Drag 'growth_rate' to Rows shelf.
- Drag 'city' and 'country' to Detail.
- Drag 'continent' to Color and 'population_2024' to Size.

_5. Total Population Change by Continent and Country_
Chart Type: Symbol Map

Create a calculated filed 'Population Change'
```tableau
    [population_2024] - [population_2023]

- Drag 'country' to Detail shelf.
- Drag 'Population Change' to Size shelf.
- Drag 'continent' to Color shelf and 'Population Change' to Label shelf.

_6. Cities with Largest Population Increase_
Chart Type: Bar Chart

- Drag 'city' to Rows shelf.
- Drag 'Population Change' to Columns shelf.
- Sort by Population Increase.
- Filter to show the Top 10 cities.

_7. Dashboard_
- Combine all visualizations into a dashboard.
- Add titles, annotations, and interactive elements like filters.
