# NYC Executed Evictions Analysis

### Project Overview

For my first data analysis project, I analyzed residential evictions in NYC from 2017 to 2023 using NYC's Open Data Evictions dataset. In my analysis, I wanted to identify residential evictions trends before, during, and after COVID-19, identify which borough(s) and zip codes have the highest number of residential evictions, which months see the highest numbers of evictions, and gain an overall better understanding of residential evictions in NYC.

### Data Sources

The primary dataset used for this analysis is the Evictions_20240102.csv file, containing a download of NYC Open Data’s Evictions dataset on January 2, 2024. The dataset contains basic data about executed evictions within the five boroughs reported by New York City Marshals, for the year 2017 - 2023. The data fields include but are not limited to Court Index Number, Docket Number, Eviction Address, Executed Date, Residential or Commercial (property type), Borough, and Zip Code.

### Tools

- SQL - Data Analysis in BigQuery
- Tableau - Data Visualization via two dashboards [Here](https://public.tableau.com/views/cleaned_distinctNYCresevictions/NYCevictionsoverview?:language=en-US&:display_count=n&:origin=viz_share_link) and [Here](https://public.tableau.com/views/2023ExecutedResidentialEvictionsintheBronxNYC/Bronxresevictionsdashboard?:language=en-US&:display_count=n&:origin=viz_share_link)

### Data Cleaning/Preparation

- Data loading and inspection: Discovered that all evictions in the dataset include an execution date (i.e. only executed evictions are represented in the dataset, not pending or scheduled executions), distinct evictions are represented multiple times (as a result of multiple court filings by landlords), and that there is no column for Scheduled Status (Pending/Scheduled) even though the description of the dataset states there is.
- Data preparation: Searched for duplicate values and identified specific columns that will query distinct eviction records. Created a temporary table to query a subset of data (distinct court index numbers, addresses, executed dates ) that will allow analysis of residential evictions. 

### Exploratory Data Analysis

I explored the evictions data to answer key questions, such as: 
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
- Two large external factors significantly impacted residential eviction activity in NYC: (a) In February of 2017, New York City implimented  Universal Access to Counsel, which guarentees free legal representation to all low-income tenants facing eviction in the City's housing courts and (b) in February of 2020, at the onset of the COVID-19 pandemic, New York State enacted a statement moratorium on any residential or commercial evictions.
- Finally, both rental housing in NYC are incredibly dynamic, constantly changing, and impacted by so many interrelated factors (market fluctuations; development, zoning, and regulatory changes; global events) that it is difficult to pin down cause-and-effect relationships without more detailed data over a longer period of time.
