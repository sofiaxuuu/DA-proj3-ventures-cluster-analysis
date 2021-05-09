# DA-proj3-ventures-cluster-analysis

## Background 
America has been the hot spot of entrepreneurship and innovation for decades, and it provides a unique environment for startups to grow. Comparing to other regions like Europe or Asia, there are much more venture capital businesses as well as angel investors willing to support new ideas. In 2018 and 2019, VCs invested around [$140 billion] (https://techcrunch.com/2021/01/19/in-2020-vcs-invested-428m-into-us-based-startups-every-day/#:~:text=In%202018%20and%202019%2C%20VCs,and%20later%2Dstage%20in%20focus). into domestic startups, making last year’s $156 billion results a record. In comparison, the [total value of venture capital investments in Europe in 2020 is around (30$ billion)] (https://www.statista.com/statistics/879080/value-of-investments-by-venture-capital-europe/). 

The difference in number also reflects in the number of startups. The number of new ventures established in the United State in 2018 is around 733K, while the number of new ventures established in Europe is 123K. [citation 1: Number of business establishments in US](https://www.statista.com/statistics/235494/new-entrepreneurial-businesses-in-the-us/) [citation 2: Number of estimated startup in Europe](https://medium.com/glassdollar/estimating-the-number-of-startups-in-europe-5d28286307f8). 

As part of a student-run startup, I'm interested in exploring the startup companies landscape in the US, and which category our current company may fall into. 

## Business Quesiton 
Business Question: __For each venture in a venture capital’s portfolio, which segment will it belongs?__

## Data Sources 
To further investigate the startup environment in U.S, I use data from Crunchbase, which is a platform for finding business information (investment, funding, founding members, etc) about private and public companies. Due to limited access to data, I use unofficial CSV exports derived from the individual worksheets from [crunchbase_export.xlsx](https://github.com/notpeter/crunchbase-data), extracted from the December 4, 2015 Crunchbase Data Export by Github user notpeter. 

More specifically, to answer my business question of “Suppose I’m in a venture capital firm, which segment of ventures will venture in my protfolio belongs?”
Ie the Data Question: **How to categorize startups in US, based on total funding received , number of rounds of funding, and days the startup is founded until December 4, 2015? ** 

 I focus one one dataset [crunchbase-companies-2015](https://github.com/sophiaxuu/DA-proj3-ventures-cluster-analysis/blob/main/companies.csv). This dataset have the following attributes: 
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
All of my data analysis is shown in the excel file: [companies.xlsx](https://github.com/sophiaxuu/DA-proj3-ventures-cluster-analysis/blob/main/companies.xlsx)

1. After converting the companies.cvs to companies.xlsx, the first step I do is data cleaning. Because I want to conduct cluster analysis of ventures based on total funding received , number of rounds of funding, and days the startup is founded until December 4, 2015, I first apply filter to “funding_total_usd”, “funding_rounds”, and “founded_at”, and ignore those with empty data. Since I’m investigating venture landscape in U.S, I only look at data where country_code is USA. There are a lot of ventures based on US, as USA has 21645 venture listed in the dataset, while China has only 564.  
2. Next, I copy filtered data to a new table named “usa_companies”. To calculate the total number of days a startup is founded until December 4, 2015, I add a new column named “days_founded” = “curr_date” - “founded_at”. 
3. Then I calculate mean and standard deviation for each attributes as follows: ![table1](https://github.com/sophiaxuu/DA-proj3-ventures-cluster-analysis/blob/main/table1.png)
4. Calculate the z-value for funding_total_usd, funding_round, and days_founded using the STANDARIZE function, and name each of them “calculate std_fundint_total_usd”, “std_funding_rounds”, “std_days_founded” respectively. 
5. Next I create a new table consisting of three random anchor numbers under “cluster anchor number”. Then I use VLOOKUP function to fill in standarlized data as well as the “cluster anchor startup name”. ![table2](https://github.com/sophiaxuu/DA-proj3-ventures-cluster-analysis/blob/main/table2.png)
6. Calculate distance between each anchors to each of the sample data points, and put results as “distsq1”, “distsq2”, and “distsq3” respectively.
7. Then I find “min_distsq” using the MIN function, and calculator the “sum of min distance squares ” using SUM function.
8. I identify each cluster nodes “cluster_anchor” using MATCH function. And my current sum of min distance squares = 6114.216154. ![table3](https://github.com/sophiaxuu/DA-proj3-ventures-cluster-analysis/blob/main/table3.png)
9. Finally, I can use the Solver tool to conduct cluster analysis. The optimal solution happens when finding: 
* Finding min value of “sum of min distance squares” 
* Change cluster anchor number with three constraints: achor number <= 21567, anchor number >=1 and anchor number is a integer number 
* And the solver solution is shown as below: 
![table4](https://github.com/sophiaxuu/DA-proj3-ventures-cluster-analysis/blob/main/table4.png)
10. Now we have three anchor points founded: 
* Catbird: lower but approximated average total funding, approximately average funding rounds, and significantly larger than average days funded 
* Array Health Solutions: lower but apprixmately average total funding, significanlty larger than average funding rounds, and larger than average days funded
* GoldCleats Global: lower average total funding, lower than average funding rounds, and larger than average days founded

To better distinguish each cluster, the following figure provide a visualization of z-value for each cluster anchor: 
![figure2](https://github.com/sophiaxuu/DA-proj3-ventures-cluster-analysis/blob/main/fig2.png)


11. To provide a better visualization of the results, I use a pie chart and a bar chart to represent each category. ![figure1](https://github.com/sophiaxuu/DA-proj3-ventures-cluster-analysis/blob/main/fig1.png)
This means that approximately half of the ventures in US belongs to category #3 of cluster, and these are the ones receive the least funding among three clusters. Approximately 30% of ventures in US belong to category #1, and approximately 19% of venture belongs to category #2.

## Interpretation 
Given the above cluster analysis, a venture capital firm can categorize ventures in its portfolio to see how its portfolio may differ from the venture landscapes in the US in 2015. A venture that is trying to improve its performance may try to observe the pattern of categories in other top VC firms. 

A startup venture owner can also try to categorize its venture and evaluate its competitiveness. Our current startup has been founded for 220 days, receives one round of funding of value 15000, and belongs to category #3. Hence, there is still a lot to improve to achieve higher competitive advantages. Since the startup falls under category #3 like GoldCleats Global, then it means that the venture is not super competitive in collecting funding as it performs similar to 50% of other ventures. 

## Future Work 
I’m not completely satisfied with the cluster analysis I achieve right now, as ideally, I want to see a cluster with a high amount of funding and a more distinct difference among clusters. Therefore, I could potentially use 4-anchor or 5-anchors cluster analysis, taking days between the venture first receive funding until now, or days the venture last receive funding until now. 

In another way, I may potentially investigate the venture landscapes in other regions like Europe and Asia. There could be some differences in the characteristics of each cluster. 

If the clustering is still similar, I would like to see how to potentially cluster startup based on non-numeric values like category and location. 


