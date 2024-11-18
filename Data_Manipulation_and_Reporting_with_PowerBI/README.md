# Zomato Global Restaurants Analysis with Power BI
![Zomato_Project-1](https://github.com/user-attachments/assets/f1508d33-69e0-410f-abb7-c581a45835b4)
## Project Overview

This project aims to uncover business insights from Zomato's global restaurant data by building an interactive Power BI dashboard. The analysis helps Zomato gauge its business performance across regions and understand restaurant metrics like ratings, cost, and cuisine offerings.

## Objectives
+ Restaurant Count Analysis: Track the number of restaurants across continents, countries, and cities.
+ Top Restaurant Performance: Identify top-rated and affordable restaurants.
+ Interactive Filtering: Filter data by region, service types, and ratings.
+ Cuisine Insights: Rank restaurants based on cuisine variety.
+ Accessibility: Ensure dashboard availability across devices for easy access.

## Workflow
1. Data Import & Transformation: Combined country-level data files into a single table, Zomato Global, removing redundant columns and errors.
2. Column Management: Merged and cleaned restaurant address columns using custom Power BI formulas to remove unwanted separators.
3. Cuisine Data Transformation: Split and expanded multiple cuisines into rows, ensuring clean data for analysis.
4. Data Cleaning: Removed nulls and duplicates, ensuring high data quality across tables.

## Data Modeling

+ Established relationships between Zomato Global and other reference tables to enhance insights.

## Key DAX Calculations

+ Rating Color: Classified restaurants by rating color code for easy visualization

#### Rating Color = IF('Fact Table'[Aggregate rating] > 4.5, "Dark Green",
#### IF('Fact Table'[Aggregate rating] >= 4 && 'Fact Table'[Aggregate rating] <= 4.4, "Green",
#### IF('Fact Table'[Aggregate rating] >= 3.5 && 'Fact Table'[Aggregate rating] <= 3.9, "Yellow",
#### IF('Fact Table'[Aggregate rating]>=2.5 && 'Fact Table'[Aggregate rating] <=3.4, "Orange",
#### IF('Fact Table'[Aggregate rating] >= 1.8 && 'Fact Table'[Aggregate rating] <= 2.4, "Red",
#### IF('Fact Table'[Aggregate rating] = 0 && 'Fact Table'[Aggregate rating] <= 1.7, "White"))))))

+ Total Restaurant Count: 
#### COUNT('Zomato Global'[Restaurant ID])
#### Average Cost for Two: AVERAGE('Fact Table'[Average Cost for two])
#### Cuisines Count: DISTINCTCOUNT('Country Wise Cuisines'[Cuisines])

+ Visualizations
1. Global View: Displayed restaurant counts across continents and countries.
2. Top Restaurants: Highlighted restaurants based on ratings and cost.
3. Interactive Filters: Users can filter data by location, services offered, and rating color codes.
4. Cuisine-Based Ranking: Ranks restaurants based on the number of cuisines offered.

## Insights Gained
+ Customer Preferences: Top-rated, affordable restaurants by region.
+ Cuisine Popularity: Trends in cuisine variety by location.
+ Geographic Insights: Distribution and accessibility of services like online ordering.
+ Explore the Power BI Dashboard for a deeper look at the visualizations.
