# Exploring Geospatial Demographics and Chicago’s Covid-19 Response
In Spring 2021, when Chicago began rolling out its first rounds of vaccines for city residents, an [article](https://www.chicagotribune.com/coronavirus/vaccine/ct-illinois-covid-vaccine-demographics-20210212-yuetcgi4mjd6terw62dljefceu-story.html) was released by the Chicago Tribune highlighting  disproportionately high rates of Covid-19 deaths among African-American residents and inequity in the distribution of vaccines. Interested in exploring the issue further and conducting more granular, neighborhood-level analysis, I engaged in the following exploratory data analysis to understand how marginalized and at-risk communities were fareing during the pandemic and how adequate the city of Chicago’s response was in distributing vaccinations. 

### Initial Questions
In my analysis of Chicago demographic and Covid-19 data, I sought to answer the following questions: 
- Which neighborhoods in Chicago have been hit the hardest by the pandemic?
- How do socioeconomic factors vary across different areas of Chicago, and how do they correspond with Covid-19 infections and mortality?
- What are the socioeconomic and geographic determinants of the vaccination administration? 

Broadly, I wanted to understand whether the hardest-hit neighborhoods are those that received vaccines first, and what underlying demographic factors might influence infections and vaccination.

### Process and Provenance
All datasets were collected from the City of Chicago [Data Portal](https://data.cityofchicago.org/) as of February 2021, and I performed data cleaning, reshaping, and visualization in Python using the Datascience, Matplotlib, Pandas, Geopandas, and Seaborn libraries. 

My data consisted of 3 datasets and qualitative geospatial information drawn from several repositories. From the Chicago Data Portal, I gathered data about Covid-19 infections, mortality, and vaccinations by zip code. Additionally, I found 2018 community data snapshots and demographic information for Chicago Community Areas from the Illinois government’s CMAP Data Hub. While Covid-19 data included geodata in the form of zip codes, the demographic data was categorized by 77 community areas. In order to bridge the gap, I researched which zip codes and community areas correspond with each “side” of Chicago, and manually entered the “region” data in each of the datasets using Excel. Before uploading the CSV files to JupyterHub, I deleted columns from the datasets not relevant to my exploratory questions. From there, my data-cleaning process primarily consisted of removing missing values and regrouping data in Python. Notably, the nine “sides” of Chicago do not precisely map on to zip code zones and community area boundaries, so there is a degree of error in the data due to the classification of border areas as being entirely included in one region.

## Exploratory Data Analysis

### Which neighborhoods in Chicago have been hit the hardest by the pandemic? 
Examining geospatial data for cumulative Covid-19 case rates per 100,000 people, which controls for absolute population differences across regions, the data reveals that the Far North Side, West Side, Southwest Side, South Side have generally experienced the highest cumulative death rates. A similar pattern emerged for cumulative case rates, with the Far North Side, West Side, and South Side having relatively high rates for cumulative Covid-19 cases; notably, however, Central also saw high rates of Covid-19 infections, whereas the South Side had the lowest cumulative case rates across Chicago. 

<p align="center">
  <img src="https://user-images.githubusercontent.com/72634325/147865341-649dd611-fdf3-49a3-8de0-5835075c7987.png" height="200" />
  <img src="https://user-images.githubusercontent.com/72634325/147865345-1b8b7d0a-4aea-4da5-b461-7c0794148641.png" height="200" /> 
  <img src="https://user-images.githubusercontent.com/72634325/147865346-ee17fff5-f7ae-4563-9192-f0978e6e6cbb.png" height="200" />
</p>

Analyzing time-series data (where Week 0 corresponds to March 1, 2020) for the nine geographic regions around Chicago reveals a similar trend, where the Southwest Side, West Side, and Far North Side have the highest rates of Covid-19 infection. However, it is interesting to note that the next highest rates for weekly cases occur in the Northwest and North Sides, which had low cumulative death rates. The opposite trend was true for neighborhoods in the South Side, where the rate of weekly cases was low over the last year,  yet the cumulative mortality rates were high.

<p align="center">
  <img src="https://user-images.githubusercontent.com/72634325/147865481-50e89c56-7be5-4b41-b514-f3450c074730.png" height="200">
  <img src="https://user-images.githubusercontent.com/72634325/147865482-9c910213-03c8-4dd4-bdee-8cfafa2a0bd5.png" height="200">
</p>

### How do socioeconomic factors vary with Covid-19 infections and mortality across different areas of Chicago?

#### Impact of Race
The racial composition of various neighborhoods in Chicago vary widely by geography; more than 55% of residents in the Central, Far North, North, and of the city were white, with the predominant minority groups being Hispanic and Asian. Proportionally, the greatest concentration of Hispanic residents lived in the Northwest, Southwest, and West sides of Chicago. Meanwhile, the southern sides of the city had the most African-American residents, with the majority and plurality of residents in the Far Southeast Side, South Side, and Far Southwest Side identifying as Black. 

<p align="center">
  <img src="https://user-images.githubusercontent.com/72634325/147865687-ee46acd6-b05a-4568-8543-82e577b8767a.png" height="180">
  <img src="https://user-images.githubusercontent.com/72634325/147865688-c8ccfb50-889e-4b05-a2b6-a026af0ba08e.png" height="180">
</p>  

Since weekly cases tend to fluctuate significantly, I used  linear regressions to analyze the relationship between race and cumulative cases. The results reveal that regions with greater proportions of White, Asian, and Hispanic residents tend to have higher cumulative Covid-19 cases, whereas a greater proportion of Black residents was associated with fewer cumulative cases.

<p align="center">
  <img src="https://user-images.githubusercontent.com/72634325/147865616-b043ca3f-836e-4c4b-a71a-89e0f15ab7ad.png" height="180">
  <img src="https://user-images.githubusercontent.com/72634325/147865617-477d8a03-6216-47b1-a602-8c9bfd7280a5.png" height="180">
</p>  

In terms of mortality, neighborhoods with proportionally greater Asian and Hispanic populations tended to witness higher cumulative death rates, whereas the reverse was true of areas with a greater proportion of Black and white residents.

<p align="center">
  <img src="https://user-images.githubusercontent.com/72634325/147865610-8ca00ebb-cc30-4138-8b1e-dd767b121326.png" height="240">
  <img src="https://user-images.githubusercontent.com/72634325/147865615-66c49f20-4ee7-4b04-9a9b-6ac24ea12476.png" height="240">
</p>

#### Impact of Age
Overall, the southern regions of the city tend to have the greatest proportion of older residents, with the Far Southwest Side, Far Southeast Side, and South Side having the highest proportion of residents who are older than 65  at 16%, 15.5%, and 14% respectively.  These also tended to be the areas with the greatest proportion of adolescents, with the Far Southeast Side, Far Southwest Side, West Side, and Southwest Side all having over 25% of residents under 19 years of age. Regions with the greatest concentration of young adults aged 20-34 were Central, the North Side, and the West Side. 

<p align="center">
  <img src="https://user-images.githubusercontent.com/72634325/147865748-877fb163-8b57-4d7d-ab33-1d2e0e92b9f3.png" height="180">
  <img src="https://user-images.githubusercontent.com/72634325/147865750-47955fb5-dcc0-4b34-a420-dc9e684f2209.png" height="180">
</p>

Using regressions to assess the relationship between the proportion of each age group and the cumulate case rates, I found that neighborhoods with a larger percentage of older residents—those 50 and older—were those with the lowest cumulative infection rates, as indicated by the negative slopes (Figure 15). On the other hand, having a greater proportion of younger residents—those under 50—was positively correlated with greater Covid-19 infection rates (Figure 14). Additionally, the regression output table for cumulative death rate versus age proportion shows that regions with more 50+ and 20-34 year-old residents tended to also have lower mortality rates, with the opposite trend true for adolescents and 35-49 year-olds (Figure 16).

<p align="center">
  <img src="https://user-images.githubusercontent.com/72634325/147865753-68c42669-7f28-4839-8551-ff0f02458e77.png" height="180">
  <img src="https://user-images.githubusercontent.com/72634325/147865754-b9bbfc35-a848-414d-b2d2-720129fa1b13.png" height="180">
</p>

#### Impact of Socioeconomic Status
Across the city of Chicago, the South Side, Far Southeast Side, West Side, and Far North Side are those with the greatest proportions of residents who earn under $50,000 each year, at 61.9%, 57.8%, 51.9%, and 43.8% respectively. The most affluent neighborhoods were located in Central and the North Side, with 60% and 48.8% of residents earning upwards of $100,000 each year. 

<p align="center">
  <img src="https://user-images.githubusercontent.com/72634325/147865915-a7eb9980-84ed-4eb8-a1e3-43bee02a983c.png" height="200">
  <img src="https://user-images.githubusercontent.com/72634325/147865918-bad965bc-285a-474f-ac27-edf8616a11e1.png" height="200">
</p>


After conducting simple linear regressions, I discovered having a higher proportion of both low and high income brackets was slightly positively associated with higher Covid-19 infection rates across Chicago’s nine regions (Figure 19). In contrast, cumulative death rates were highest in neighborhoods with greater proportions of residents who earned under $50,000 each year, and areas with more affluent residents were those with lower mortality rates.

<p align="center">
  <img src="https://user-images.githubusercontent.com/72634325/147865937-96338c3a-95dc-4afe-9399-10eded24d305.png" height="180">
  <img src="https://user-images.githubusercontent.com/72634325/147865939-b16d4c5c-b1f0-480d-9790-90f18e57315b.png" height="180">
</p>

### What are the socioeconomic and geographic determinants of the vaccination administration?

Across Chicago, the greatest percent of residents have been vaccinated in Central, the North Side, and the Far North Side. These geospatial patterns hold when measuring both cumulative doses and first doses. From comparing vaccination rates to prior demographic analysis, the data illuminates that these areas have the top 3 highest proportions of white residents, at between 55 to 70 percent, have relatively low senior populations but a high density of millennials, and are the three most affluent areas in the city of Chicago, with the highest rates of residents earning over $100,000 annually—results corroborated by the figures majority dominant demographics in each region. The areas with the lowest percent of vaccinated residents are the Far Southeast Side, Southwest Side, and Northwest Side, which have a plurality of residents who are Black or Hispanic, earn under $50,000 a year, and high relative percentages of residents in their 50’s and older.

<p align="center">
  <img src="https://user-images.githubusercontent.com/72634325/147865978-d7a66772-525b-4fc2-a5c8-daa7c2f88fc1.png" height="240">
  <img src="https://user-images.githubusercontent.com/72634325/147865981-95971ca4-7ccc-4ff9-9976-0c8c2ad08e3a.png" height="240">
  <img src="https://user-images.githubusercontent.com/72634325/147865986-547f6112-aad2-4517-94a6-a422212fa696.png" height="240">
</p>

### Takeaways and Implications

Race: Taken together, the exploratory visualizations suggest that the regions of Chicago with the greatest number of Covid-19 infections also happen to be those with greater proportions of White, Asian, and Hispanic residents. As shown by the regression output table for race distributions, however, the results are not robust due to the small sample size of only 9 regions, which accounts for the non-significant slope results, low correlations, and wide 95% confidence intervals. Examining the geospatial plots yields more salient results, namely that there are no clear racial patterns for where the brunt of Covid-19 infections and deaths have occurred. The Far North Side, West Side, and Southwest Side experienced the greatest death rates, but respectively were majority white, Black, and Hispanic. The same holds true for cumulative Covid-19 cases.

<p align="center"> 
  Regression Output for Race and Case Rates 
</p>

<p align="center">
  <img src="https://user-images.githubusercontent.com/72634325/147866060-7a17372b-9c8a-467d-ba9a-80af18481ce5.png"  width="600">
</p>
                                                                                                                        
The greatest racial disparities emerge for vaccination, where predominantly white neighborhoods received a proportionally greater percentage of the vaccine; even with only 9 data points, the regression slopes for the percent of white, Hispanic, and Asian residents and cumulative vaccination rates were significant. Only greater percentages of white and Asian residents were correlated with a higher rate of community vaccination. Thus, there may indeed be racial disparities at play when it comes to the administration of vaccines. Nevertheless, the negative association between the percent of Black residents and Covid-19 infections and deaths complicates a clear-cut picture of discrimination.
                                                                                                                           
<p align="center">  Regression Output for Race and Vaccination Rates </p>

<p align="center">
  <img src="https://user-images.githubusercontent.com/72634325/147866063-abcafe14-e1f1-49c7-b2da-21367b384e09.png" width="600">
  </p>

Age: Neighborhoods with a greater proportion of elderly residents—the most at-risk age group—are those that experienced the lowest rates of Covid-19 infections and mortality, contrary to what one might expect. The data indicates that neighborhoods with more middle-aged and senior residents may be those where cumulative cases are the lowest due to greater caution on the part of residents, whereas younger neighborhoods are those where residents exercised less caution or faced greater Covid-19 exposure. Interestingly, the regions of Chicago with the highest proportion of vaccinated residents are those with the largest population of young adults. As with the racial demographic data, bootstrap results were non-significant. However, the exploratory data indicates that either older residents may be more hesitant to receive the Covid-19 vaccine, lack access to vaccination facilities, or are receiving the vaccine at a lower rate for other reasons despite having first priority per Chicago policy.

Income: Although the slopes for cumulative case rates versus income are rather flat, generally more affluent areas are those with the greatest proportion of vaccinated residents, moderate rates of Covid-19 infection, and relatively low death rates. However, due to the small sample size and less granular classification (only 3 categories), it is difficult to definitely claim that wealthier neighborhoods are those that are receiving the vaccine first despite being those that may need it the least when it comes to mortality.

