# NYC Executed Evictions Analysis

### Project Overview

For my first data analysis project, I analyzed evictions in NYC from 2017 to 2023 using NYC's Open Data Evictions dataset. In my analysis, I wanted to identify residential evictions trends before, during, and after COVID-19, identify which borough(s) and zip codes have the highest number of residential evictions, which months see the highest numbers of evictions, and gain an overall better understanding of residential evictions in NYC. My overall goal with the project was to practice basic SQL queries on a government dataset and create my first dashboard in Tableau.

### Data Sources

The primary dataset used for this analysis is the Evictions_20240102.csv file, a download of NYC Open Data’s Evictions complete dataset on January 2, 2024. The dataset contains basic data about executed evictions within the five boroughs reported by New York City Marshals, for the years 2017 - 2023. The data fields include but are not limited to Court Index Number, Docket Number, Eviction Address, Executed Date, Residential or Commercial (property type), Borough, and Zip Code.

### Tools

- SQL - Data Analysis in BigQuery
- Tableau - Data Visualization via two dashboards, [here](https://public.tableau.com/views/cleaned_distinctNYCresevictions/NYCevictionsoverview?:language=en-US&:display_count=n&:origin=viz_share_link) and [here](https://public.tableau.com/views/2023ExecutedResidentialEvictionsintheBronxNYC/Bronxresevictionsdashboard?:language=en-US&:display_count=n&:origin=viz_share_link)

### Data Cleaning/Preparation

- Data loading and inspection: Discovered that all evictions in the dataset include an execution date (i.e. only executed evictions are represented in the dataset, not pending or scheduled executions), distinct evictions are represented multiple times (as a result of multiple court filings by landlords), and that there is no column for Scheduled Status (Pending/Scheduled) even though the description of the dataset states there is.
- Data preparation: Searched for duplicate values and identified specific columns that will query distinct eviction records. Created a temporary table to query a subset of data (distinct court index numbers, addresses, executed dates ) that will allow analysis of residential evictions. 

### Exploratory Data Analysis

I explored the eviction data to answer key questions, such as: 
- What did residential evictions look like before, during, and after COVID-19?
- Which borough(s) and zip codes have the highest number of residential evictions?
- Are there specific months of the year that have the highest number of residential evictions?

### Data Analysis

TK interesting SQL queries

### Results/Findings
The analysis results are sumarized as follows:
1. Despite a spike in evictions following the end of the COVID-19 eviction moratorium in early 2022, eviction numbers have remained below the pre-pandemic averages: total evictions in 2023 is 42% lower than the total in 2017.
2. Since 2017, Bronx has had the highest number of executed residential evictions each year except for 2021 & 2022, where Brooklyn had the highest. Bronx's residential evictions in 2023 were 66% higher than the City-wide average number of executed residential evictions.
3. Comparing evictions numbers for the year 2017 to the year 2023, Queens (55.2%) and Bronx (46%) showed the biggest reductions in executed residential evictions, 55.2% and 46%, respectively. Manhattan showed the lowest reduction in executed residential evictions (22.5%) followed by Staten Island (27.3%).
4. Citywide, January and August are the months with the highest numbers of executed evictions. In the Bronx, it’s January and May.

### Limitations
The NYC Open Data's Evictions dataset and my analysis have several limitations:
- The dataset does not include eviction data prior to January 1, 2017.
- Three large external factors significantly impacted residential eviction activity in NYC: (a) In February of 2017, New York City implimented  Universal Access to Counsel, which guarentees free legal representation to all low-income tenants facing eviction in the City's housing courts, (b) COVID-19 pandemic, and (c) in February of 2020, at the onset of the COVID-19 pandemic, New York State enacted a statement moratorium on any residential or commercial evictions.

## Insights
- Although it's clear that residential evictions are trending downwards since 2017, it's difficult to drawn meaningful insights because of the relatively small timeframe combined with the external factors listed above.
- Rental housing in NYC is also incredibly dynamic, constantly changing, and impacted by several interrelated factors (market fluctuations; development, zoning, and regulatory changes; global events like COVID-19; etc). Likewise, evictions are impacted by several different interrelated factors including but not limited to housing affordability and the legal and policy environment in the area at a particular time.

- Although it's clear what factors make individuals and families more likely to face eviction, it's unclear what the most effective strategies at preventing evictions in the first place.   

## Conclusion
Overall, this project provided me with great, hands-on practice in learning SQL on a topic I'm passionate about: housing! Tableau has a steep learning curve (for me, at least) and I struggled to do seemingly simple things (like manually adjusting the width of a cell!), but I now have a much better understanding of the software after creating two dashboards for this project.   
