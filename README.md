# DA-proj3-ventures-cluster-analysis

## Background 
America has been the hot spot of entrepreneruship and innovation for decades, and it provides a unique environment for startups to grow. Comparing to other regions like Europe or Asia, there are much ore venture capital companies as well as angel investors willing to support new ideas. During the first three quarters of 2019, global venture capital investments reached over 161 billion U.S dollars with the United States accounting for more than half of all VC investments made worldwide. In terms of per capita spend, of all major VC investment markets it was Israel that came out on top with over 414 U.S dollars per capita in venture capital investments per capita (https://www.statista.com/statistics/1071105/value-of-investments-by-venture-capital-worldwide-by-key-market/#statisticContainer). 

Interested in entrepreneurship, I would like to explore further into the startup companies landscape. 

## Business Quesiton 
Business Question: __Suppose I’m in a venture capital firm, which segment of ventures will venture in my protfolio belongs?__

## Data Sources 
To further investigate the startup environment in U.S, I use data from Crunchbase, which is a platform for finding business information (investment, funding, founding members, etc) about private and public companies. Due to limited access to data, I use unofficial CSV exports derived from the individual worksheets from crunchbase_export.xlsx, extracted from the December 4, 2015 Crunchbase Data Export by Github user notpeter (https://github.com/notpeter/crunchbase-data). 

More specifically, to answer my business question of “Suppose I’m in a venture capital firm, which segment of ventures will venture in my protfolio belongs?”
Ie the Data Question: How can I categorize startups in US, based on total funding received , number of rounds of funding, and days the startup is founded until December 4, 2015? 

 I focus one one dataset [crunchbase-companies-2015] (https://github.com/sophiaxuu/DA-proj3-ventures-cluster-analysis/blob/main/companies.csv). This dataset have the following attributes: 
- permalink: permanent link to the venture description 
- name: name of the venture 
- homepage_url	: link to venture’s own website
- category_list: list of categories of the venture
- funding_total_usd: total funding received in USD 
- status: status of the venture (operating, closed, or acquired) 	
- Country_code: code of the country where venture belong
- State_code: code of state
- region	
- city	
- funding_rounds: count of number of funding rounds the venture gets
- Founded_at: time when the venture is founded 
- First_funding_at: first time when venture receive funding
- Last_funding_at: the most recent time when venture receive funding

## Cluster Analysis 
1. After converting the companies.cvs to companies.xlsx, the first step I do is data cleaning. Because I want to conduct cluster analysis of ventures based on total funding received , number of rounds of funding, and days the startup is founded until December 4, 2015, I first apply filter to “funding_total_usd”, “funding_rounds”, and “founded_at”, and ignore those with empty data. Since I’m investigating venture landscape in U.S, I only look at data where country_code is USA. There are a lot of ventures based on US, as USA has 21645 venture listed in the dataset, while China has only 564.  

2. Next, I copy filtered data to a new table named “usa_companies”. To calculate the total number of days a startup is founded until December 4, 2015, I add a new column named “days_founded” = “curr_date” - “founded_at”. 

3. Then I calculate mean and standard deviation for each attributes as follows: 







