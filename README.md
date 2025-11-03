# -World-Bank-Development-Indicators Analysis

### Project Overview
This is an analysis of Different countries Development Indicators as published by World bank data from year 1960 - 2018. It reveals insights on how Topp countries are performing using various indicators across different years, different regions, different economic or income gruops.

### Data Sources
The primary data source that was used for this analysis is "WorldBank.xlsx" file and was downloaded from kaggle.com

### Tools
- Jupyter Notebook was Used for the analysis
- Python was primarily used for the data cleaning, data exploration, data visualiztion was done using plotly

### Data Cleaning and Preparation
During the data cleaning phase the various tasks where performed
1. Data Loading and inspection
2. Checking for missing values
3. Droping of columns with excessive missing values after setting a threshold
4. Replacing of numerical missing values with the median and replacing categorical missing values with the mode

### Exploratory Data Analysis
-  Number of countries and regions
-  List Of unique Countries and Regions
-  Distribution of different income or economic group of countries
-  Years covered in the data collection
-  Top 5 countries by GDP per capita (latest year available)
-  Average life expectancy by region (latest year available)
-  Correlation between GDP per capita and Life expectancy in each country
-  Countries with highest and lowest infant mortality rate (latest year)

### Sample of code used

``` python
# 1. Number of countries and regions
num_countries = world_bank_df['Country Name'].nunique()
num_regions = world_bank_df['Region'].nunique()

#2.List Of Countries and Regions
unique_countries = world_bank_df['Country Name'].unique()
unique_regions = world_bank_df['Region'].unique()

# 2. Distribution of income groups
income_group_counts = world_bank_df['IncomeGroup'].value_counts()

# 3. Years covered
years_covered = world_bank_df['Year'].min(), world_bank_df['Year'].max()
print(years_covered)

# 4. Missing data overview
missing_data = world_bank_df.isnull().sum().sort_values(ascending=False)

# 5. Summary statistics for key indicators
summary_stats = world_bank_df.describe(include='all')

# 6. Top 5 countries by GDP per capita (latest year available)
latest_year = world_bank_df['Year'].max()
top_gdp_per_capita = world_bank_df[world_bank_df['Year'] == latest_year].nlargest(5, 'GDP per capita (USD)')[['Country Name', 'GDP per capita (USD)']]
#print("Top 5 countries by GDP per capita (latest year):")
#print(top_gdp_per_capita)


# 7. Average life expectancy by region (latest year available)
avg_life_expectancy = world_bank_df[world_bank_df['Year'] == latest_year].groupby('Region')['Life expectancy at birth (years)'].mean().sort_values(ascending=False)
#print("\nAverage life expectancy by region (latest year):")
#print(avg_life_expectancy)

# 8. Correlation between GDP per capita and Life expectancy
correlation = world_bank_df[['GDP per capita (USD)', 'Life expectancy at birth (years)']].corr().iloc[0,1]
#print(f"\nCorrelation between GDP per capita and Life expectancy: {correlation:.2f}")

# 9. Countries with highest and lowest infant mortality rate (latest year)
infant_mortality = world_bank_df[world_bank_df['Year'] == latest_year][['Country Name', 'Infant mortality rate (per 1,000 live births)']]
highest_infant_mortality = infant_mortality.nlargest(1, 'Infant mortality rate (per 1,000 live births)')
lowest_infant_mortality = infant_mortality.nsmallest(1, 'Infant mortality rate (per 1,000 live births)')

```
### Result and Findings
- The Top 3 Countries Highest Birth rate on the average respectively
    - India
    - Brazil
    - China
- The top 3 Countries Death rate on the average respectively
    - Germany
    - Italy
    - United Kingdom
- Countries with Highest Life Expentancies are those in High income groups. The higher the income group the higher the life expectancy
- Top country with the highest GDP in 2018
    - USA
    - China
    - Japan 
