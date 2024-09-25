# PowerBI_Projects

1. Project Name : Zomato Global Restaurants Analysis with Power BI

This Power BI project aims to analyze global restaurant data, focusing on transforming, cleaning, and modeling data to provide insights into restaurant ratings, costs, and cuisines across different countries and continents. The dataset consists of eight files with restaurant data from different countries.

Project Workflow

1. Data Import and Transformation
Imported all the Excel files into Power BI.
Combined all the country-level files into a single table called Zomato Global using the "Append Queries" feature.
Corrected city name errors using the Replace Value option.
Removed redundant columns like locality and locality verbose, as this information was already present in the restaurant address.

2. Column Splitting and Merging
Split the Restaurant Name, Address column using a delimiter but mistakenly selected "each occurrence of the delimiter" instead of the "leftmost delimiter," resulting in multiple column splits.
To resolve the issue, I merged these columns back while eliminating unwanted commas by using a custom formula:

= Text.Combine(List.Select({[#"Restaurant Name,Address.2"], [#"Restaurant Name,Address.3"],[#"Restaurant Name,Address.4"],[#"Restaurant Name,Address.5"],[#"Restaurant Name,Address.6"],[#"Restaurant Name,Address.7"],[#"Restaurant Name,Address.8"]}, each _ <> null and _ <> ""), ",")

This step ensured that null and blank values were handled properly, and the problem was resolved.

3. Cuisines Data Transformation
Created a reference table named Cuisines_by_restaurant by duplicating the original table.
Removed all columns except for Restaurant ID and Cuisines.
Used the split column feature to separate multiple cuisines listed in a single cell using a comma delimiter, then expanded these into rows for a cleaner structure.
Applied Trim to remove any extra spaces in the Cuisines text.

4. Data Cleaning
Removed null, blank, and duplicate values from the Country Code table to ensure consistency and data quality.
Ensured that only the Zomato Global table was visible after the transformation, hiding other unnecessary tables.
Closed and applied the changes, finalizing the data cleaning process.

Data Modeling
Deleted unnecessary relationships between the fact table and the country-wise cuisines table.
Established a relationship between Zomato Global (Restaurant ID) and Country Wise Cuisines (Restaurant ID).

DAX Calculations
Added a New Column for Rating Colors in the fact table using this formula:

Rating Color = IF('Fact Table'[Aggregate rating] > 4.5, "Dark Green",
IF('Fact Table'[Aggregate rating] >= 4 && 'Fact Table'[Aggregate rating] <= 4.4, "Green",
IF('Fact Table'[Aggregate rating] >= 3.5 && 'Fact Table'[Aggregate rating] <= 3.9, "Yellow",
IF('Fact Table'[Aggregate rating]>=2.5 && 'Fact Table'[Aggregate rating] <=3.4, "Orange",
IF('Fact Table'[Aggregate rating] >= 1.8 && 'Fact Table'[Aggregate rating] <= 2.4, "Red",
IF('Fact Table'[Aggregate rating] = 0 && 'Fact Table'[Aggregate rating] <= 1.7, "White"))))))
Created the following measures:

Total Restaurant Count:
Total Restaurant = COUNT('Zomato Global'[Restaurant ID])

Average Cost for Two:
Average Cost = AVERAGE('Fact Table'[Average Cost for two])

Average Rating:
Average Rating = AVERAGE('Fact Table'[Aggregate rating])

Cuisines Count:
Cuisines Count = DISTINCTCOUNT('Country Wise Cuisines'[Cuisines])

Created a Continent Column in the Country Code table using the following formula to map countries to their respective continents:

Continent = SWITCH('Country Code'[Country Code],
   189,"Africa",
   215,"Europe",
   37,"NAM", 
   216,"NAM", 
   30,"SAM", 
   14,"Oceania", 
   148,"Oceania", 
   "Asia")

Visualizations you can see here, 
The following visualizations were created to provide insights based on the data:

Global View:

Displayed restaurant information across continents and countries.
Top Restaurants by Rating and Cost:

Showcased the best performing restaurants based on customer ratings and the lowest average cost.
Filters:

Enabled filtering by geographic dimensions like continent, country, and city.
Added filters based on restaurant services (online delivery, table booking) and rating colors.
Final Report and Navigation
A multi-page report was created with easy navigation and a theme that matches the company's branding. The report allows users to:

Analyze restaurant details at a global level.
Drill down into specific countries and cities to view restaurant performance.
Identify top-ranking restaurants based on ratings, cost, and number of cuisines served.
