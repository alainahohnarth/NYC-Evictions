# NYC Executed Evictions Analysis

### Project Overview

For my first data analysis project, I analyzed evictions in NYC from 2017 to 2023 using NYC's Open Data Evictions dataset. In my analysis, I wanted to identify residential evictions trends before, during, and after COVID-19, identify which borough(s) and zip codes have the highest number of residential evictions, which months see the highest numbers of evictions, and gain an better understanding of residential eviction trends in NYC. My overall goal with the project was to practice basic SQL queries on a government dataset and create my first dashboard in Tableau.

### Data Sources

The primary dataset used for this analysis is the Evictions_20240102.csv file, a download of NYC Open Data’s Evictions complete dataset on January 2, 2024. The dataset contains basic data about executed evictions within the five boroughs reported by New York City Marshals, for the years 2017 - 2023. The data fields include but are not limited to Court Index Number, Docket Number, Eviction Address, Executed Date, Residential or Commercial (property type), Borough, and Zip Code.

### Tools

- SQL - Data Analysis in BigQuery
- Tableau - Data Visualization via two dashboards, [here](https://public.tableau.com/views/cleaned_distinctNYCresevictions/NYCevictionsoverview?:language=en-US&:display_count=n&:origin=viz_share_link) and [here](https://public.tableau.com/views/2023ExecutedResidentialEvictionsintheBronxNYC/Bronxresevictionsdashboard?:language=en-US&:display_count=n&:origin=viz_share_link)

### Data Cleaning/Preparation

- Data loading and inspection: Discovered that all evictions in the dataset include an execution date and therefore distinct executed evictions are represented multiple times (as a result of multiple court filings by landlords). There is no column for Scheduled Status (Pending/Scheduled) in the dataset even though the description of the dataset states there is.
- Data preparation: Searched for duplicate values and identified specific columns that will query distinct eviction records. Created a temporary table to query a subset of data (distinct court index numbers, addresses, executed dates ) that will allow analysis of distinct, residential evictions. 

### Exploratory Data Analysis

I explored the eviction data to answer key questions, such as: 
- What did residential evictions look like before, during, and after COVID-19?
- Which borough(s) and zip codes have the highest number of residential evictions?
- Are there specific months of the year that have the highest number of residential evictions?

### Data Analysis

Here are a handful of SQL queries I used during my project:

Cleaning query:
```sql
SELECT 
Court_Index_Number, COUNT(DISTINCT Eviction_Address ) AS distinct_address_count
FROM `nyc-eviction-data.NYC_evictions_downloaded_20240102.NYC_evictions` 
GROUP BY
  Court_Index_Number
HAVING
  COUNT(DISTINCT Eviction_Address) > 1;
```

Processing via temporary table: 
```sql
CREATE TEMP TABLE temp_unique_evictions AS
SELECT
  DISTINCT Court_Index_Number,
  Eviction_Address,
  Executed_Date,
  Borough
FROM
  nyc-eviction-data.NYC_evictions_downloaded_20240102.NYC_evictions
WHERE
  Residential_Commercial = 'Residential';
```

Analysis:
```sql
SELECT
  Borough,
  EXTRACT(YEAR FROM Executed_Date) AS Year,
  COUNT(*) AS total_unique_residential_evictions
FROM
  temp_unique_evictions
GROUP BY
  Borough, Year
ORDER BY
  Borough, Year;
```

### Results/Findings
The analysis results are sumarized as follows:
1. Despite a spike in evictions following the end of the COVID-19 eviction moratorium in early 2022, eviction numbers have remained below the pre-pandemic averages: the sum of evictions in 2023 is 42% lower than in 2017.
2. Since 2017, Bronx has had the highest number of executed residential evictions each year except for 2021 & 2022, where Brooklyn had the highest. Bronx's residential evictions in 2023 were 66% higher than the City-wide average number of executed residential evictions.
3. Comparing evictions numbers for the year 2017 to the year 2023, Queens and Bronx showed the biggest reductions in executed residential evictions at 55% and 46%, respectively. Manhattan showed the lowest reduction in executed residential evictions (22.5%) followed by Staten Island (27.3%).
4. Citywide, January and August are the months with the highest number of executed evictions. In the Bronx, it’s January and May.

### Limitations
The NYC Open Data's Evictions dataset and my analysis have several limitations:
- The dataset does not include eviction data prior to January 1, 2017.
- Three large external factors significantly impacted residential eviction activity in NYC: (a) In February of 2017, New York City implimented  Universal Access to Counsel, which guarentees free legal representation to all low-income tenants facing eviction in the City's housing courts, (b) COVID-19 pandemic, and (c) in February of 2020, at the onset of the COVID-19 pandemic, New York State enacted a statement moratorium on any residential or commercial evictions.

## Insights
- Although it's clear that residential evictions are trending downwards since 2017, it's difficult to drawn meaningful insights from this dataset because of the relatively small timeframe, the external factors listed above, and the extremely dynamic nature of rental housing in NYC.
- However, [NYU Furman Center](https://furmancenter.org/research/publications/eyJyZXN1bHRfcGFnZSI6InJlc2VhcmNoXC9wdWJsaWNhdGlvbnMiLCJvcmRlcmJ5X3NvcnQiOiJlbnRyeV9kYXRlfGRlc2MiLCJrZXl3b3JkcyI6ImV2aWN0aW9ucyIsInNob3J0Y3V0IjoiZXlKeVpYTjFiSFJmY0dGblpTSTZJbkpsYzJWaGNtTm9YQzl3ZFdKc2FXTmhkR2x2Ym5NaUxDSnZjbVJsY21KNVgzTnZjblFpT2lKc2IzZGZjMlZoY21Ob1gzTmpiM0psZkdSbGMyTWlMQ0pyWlhsM2IzSmtjeUk2SW1WMmFXTjBhVzl1Y3lKOSJ9) and [Eviction Lab at Princeton University](https://evictionlab.org/research/) have conducted extensive, rigorous research on evictions in NYC using housing court records and other data to analyze eviction filings versus execution rate, rent amount sought in eviction filings, and the effects of Universal Access to Counsel on tenant outcomes.
- Evictions are a multivariant issue with crushing consequences for individuals and families and more research and funding is needed to better target resources and preventive services for those most at risk of evictions. 

## Conclusion
Overall, I learned a lot completing this project and it provided me with great, hands-on SQL practice on a topic I'm interested in--housing! Even though it's well known that 80% of data analysis is cleaning, I was still surprised by how much time it took and how essential proper cleaning was to understand the data before attempting to analyze it (I learned this the hard way, unfortunately). For me, Tableau had a steep learning curve and I struggled to do seemingly simple things (like manually adjusting the width of a cell!), but after creating two dashbaords, I now have a much better understanding of how the software works. There are several things I would change about this project if I had to do it again, but I'm ready to move on to a new project. Onwards and upwards.
