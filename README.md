# LITA-CAPSTONE-CUSTOMER-DATA-PROJECT

## Context

[Project Overview](#project-overview)

[Data Source](#data-source)

[Project Objective](#project-objective)

[Data Cleaning and Exploratory Data Analysis](#data-Cleaning-and-exploratory-data-analysis)

[Data Tools and Methods Used](#data-tools-and-methods-used)

[Data Analysis](#data-analysis)

[Data Visualization](#data-visualization)

## Project Overview
This project focuses on analyzing customer data for Petal Internet Service Provider, a subscription service with the aim of gaining insights and understanding customer behavior, preferences, trends, tracking subscription types and pinpointing key parterns in cancellations and renewals.  

## Data Source
The data used for this sales analysis was collected from the Petal Internet Service Provider's Internal CRM and Billing Systems.
- Data Collected:
1. Custormer ID
2. Custormer Name
3. Region
4. Subscription Type
5. Subscription Start Date
6. Subscription End Date
7. Subscription Cancellation
8. Revenue
- Timeframe: Data from 31st of January 2022 to 31st of August 2024

## Project Objective
The objective of the project was to analyzing customer data for Petal Internet Service Provider, a subscription service with the aim of gaining insights and understanding customer behavior, preferences, trends, tracking subscription types and pinpointing key parterns in cancellations and renewals.  Through this project, the service provider can optimize market and retention strategies as well as making imformed decisions that would help grow the service, improve customer service and boost retention. 

## Data Cleaning and Exploratory Data Analysis (EDA)
- EDA alongside data cleaning was performed in this project to understand the dataset's structure, identify and handle missing values and address any data quality issues.
  * The data was checked for duplicates by highlighting the whole data in an excel sheet and clicking on the 'Remove Duplicates' in the Data tab interface.
  * Data quality was checked for in the data when it was uploaded in Power Bi to check for any errors in the data.
- EDA also invoves the exploring of Data to answer the some questions about the Data, which are to determine;
  * Region by Total Revenue
  * Total Revenue by Subscription Type
  * Percentage of Total Revenue by Subscription Type
  * Active and Cancelled Subscription by each Region
  * Total Number of Customers by Subscription Type
  * Total Revenue generated Yearly
  * The most popular Subscription Type by the number of Customers
  * Customers who cancelled their Subscription within 6 months
  * Average Subscription Duration for all Customers
  *  Custormers with Subscription longer than 12 months
  * Total Number of Active and Cancelled Subscription by each Region
    
## Data Tools and Methods Used
1. Microsoft Excel 
- For Data Cleaning
- For Analysis utilizing Pivot Tables to summarize and analyze the dataset making it easier to identify insights
- For Visualization - Bar charts were used to visually represent key insights
2. Structured Query Language(SQL) for Quering of Data
3. Power BI used for converting data from different data sources to interactive dashbords and BI reports.
  
## Data Analysis
- ### Excel formulars used
- SubscriptionEnd Date Minus SubscriptionStart Date
- AVERAGE(number1,[number2],..): This formular was used to calculate the Average Subscription Duration
  ```AVERAGE(J2:J33788)```
![Screenshot (153)](https://github.com/user-attachments/assets/5f7c5493-a58f-45a9-9d23-3f28af9f6ea1)
- COUNTIF(range, criteria): Used to find the most popular Subscription Type,which is Basic Subscription Type
   ```COUNTIF(D2:D33788,D2)``` - Basic
   ```COUNTIF(D2:D33789,D5)``` - Standard
   ```COUNTIF(D2:D33790,D3)``` - Premium
![Screenshot (151)](https://github.com/user-attachments/assets/a1f35b00-e1e3-44ea-a19a-0a1cd954515d)

- ### SQL queries executed
- Retrive the Total Number of Customers from each Region
```SQL
Select Region, Count(CustomerID) As Total_No_Customers
From Customer_Data
Group by Region
Order by 2 Desc
```
- Find the most popular subscription type by the number of customers
```SQL
Select Top 1 SubscriptionType, Count(CustomerID) As Total_Customers
From Customer_Data
Group by SubscriptionType
```
- Find customers who canceled their subscription within 6 months
```SQL
Select CustomerID, CustomerName, SubscriptionStart, SubscriptionEnd, Canceled,
Datediff(Month, SubscriptionStart, SubscriptionEnd) As Subscription_Duration
From Customer_Data
Where Canceled = 'True' and Datediff(Month, SubscriptionStart, SubscriptionEnd)<=6
```
- Calculate the average subscription duration for all customers
```SQL
Select Avg(Datediff(Day, SubscriptionStart, SubscriptionEnd)) As Average_Subscription_Duration
From Customer_Data
```
- Find customers with subscriptions longer than 12 months
```SQL
Select CustomerID, CustomerName, SubscriptionStart, SubscriptionEnd, 
Datediff(Month, SubscriptionStart, SubscriptionEnd) as Subscription_Length
From Customer_Data
Where Datediff(Month, SubscriptionStart, SubscriptionEnd)>12
```
- Calculate total revenue by subscription type
```SQL
Select SubscriptionType, Sum(Revenue) as Total_Revenue
From Customer_Data
Group by SubscriptionType
```
- Find the top 3 regions by subscription cancellations
```SQL
Select Top 3 Region, Count(Canceled) as Subscription_Cancelled
From Customer_Data
Where Canceled = 'True'
Group by Region
```
- Find the total number of active and canceled subscriptions
```SQL
SELECT COUNT(CustomerID) as Total_No_Of_Active_Subscription 
FROM Customer_Data
where Canceled = 'False'
```

```SQL
SELECT COUNT(CustomerID) as Total_No_Of_Canceled_Subscription 
FROM Customer_Data
where Canceled = 'True'
```
- ### Dax Functions
They are functions used to perform calculations and data analysis in Power BI.
1. Measures - used to generate and callout certain valuesin reports and dashboards.
   - Calculate Average Revenue
     ```Dax
     Average Revenue = Avg(CustomerData[Revenue])
     ```
     - Calculate the Number of Custormers
        ```Dax
       Customer Count = Count(CustomerData[Customrer Name])
        ```
  - Calculate Canceled Subscription Rate
        ```Dax
       Canceled Subscription Rate = Sum(CustomerData[Canceled Subscription Count])/Sum(CustomerData[Custormer Count])
        ```
2. Calculated Columns : Conditional Function
  - Calculate Canceled Subscription Count

|Heading 1|Heading 2|Heading 3|Heading 4|
|---------|---------|---------|---------|
|Column Name|Operator|Value|Output|
|Canceled|equals|True|1|
|Else 0|


 - Calculate Active Subscription Count
   
|Heading 1|Heading 2|Heading 3|Heading 4|
|---------|---------|---------|---------|
|Column Name|Operator|Value|Output|
|Canceled|equals|False|1|
|Else 0|



## Data Visualization 
## 1. Region by Total Revenue - Microsoft Excel
## Pivot Table 1
![Screenshot (87)](https://github.com/user-attachments/assets/4a1dcb89-4ea7-4ce3-8a53-51ca0fd24a37)
## Pivot Table 2 - Total Revenue generated Yearly 
![Screenshot (95)](https://github.com/user-attachments/assets/4c3a016b-52f2-482e-9280-d5a4fc8493f7)

## Filtered Column  Chart for 2023
![Screenshot (140)](https://github.com/user-attachments/assets/42fe1ee0-da5d-4490-a95a-117bf5741d04)
## Filtered Column  Chart for 2024
![Screenshot (141)](https://github.com/user-attachments/assets/1e4d0b6e-31ca-43b1-91eb-86d993658c26)
### i. Inferences
- #### Overall Overview on Regional Revenue Performance;
Overall, the total revenue generated by the regions decreased in 2024. The pivot table 2 shows the total sales generated each year. The total revenue generated by the regions in 2024 was slightly above half of the total revenue generated in 2023.
- #### Sales Performance for each region;
  * East: East region generated the highest revenue in 2023 which indicates strong market prensence which may have been due to Petal's internet network reliability coverage. It generated the lowest revenue this year which may suggest increased competition and also ecenomic challenges such as rising inflation and decrease in cusomer spending.
  * West: The chart shows that west region is taking the lead among the regions in generating revenue this year and it generated the least sales in 2023. The increase this year might be due to improved nextwork reliability.
  * North: North seems to show a stable growth in 2024. 
  * South: The second leading region in generating sales in the year 2024.
### ii. Strategic Recomendations
- Pestel Internet providers should invest in infrastructure to expand and improve their network reliability in all the regions which can reduce interruptions in the internect connection provided to the customers
- They can also create retention initiations e.g discounts and service upgrades to encourage customers to stay.

### iii. Conclusion
- To unlock the revenue potential in all the regions, Petal Internet Service Providers should focus on expanding infrastructure, improving network reliability, offering competitive pricing and improve on customer service.

## 2. Total Number of Customers from each region - SQL
![Screenshot (108)](https://github.com/user-attachments/assets/794ab4a6-bb41-4c34-a0d6-fb3cc8b53fe7)
## Pivot Table - Microsoft Excel
![Screenshot (93)](https://github.com/user-attachments/assets/554c709f-44a1-4e69-ac05-042ce5fad944)
### i. Inferences
- #### Customer Distribution by Region;
  * The SQL query return shows that East region has the highest number of customers and West region has the lowest number of customers.
- #### Customer Loyalty Partterns;
  * East region exhibits strong customer loyalty as shown in the pivot table. In that no customer cancelled their subscription in both years, likely due to pupulation density and high demand for reliable internet services as well ascustomer satisfaction.
  * North, South and West regions have lowercustomer retention, looking at the fact that the number of customers that left the service is more than the returning and active customers indicating possible challenges in customer satisfaction.

### ii. Strategy Recommendations
- Petal Internet Service Provider should invest in infrastructure upgrades to reduce service interuptions especially during peak usage hours and offer promotional rates for the East region so as to retain customers.
- In North, South and West regions, the internet provider should invest in network expansion to improve speed and reliability, provide affordable subscription plans/types and flexible payment options to attract customers with limitedbudgets.
- They can also offer internet and Tv or internet and phone bundles to appeal to households interested in comprehensive services.
  
### iii. Conclusion
- Investing in infrastructure upgrade, investing in improving network reliability and introducing promotions will help in retaining and attracting new customers.

## 3. Total Revenue by Subscription Type - SQL

![Screenshot (106)](https://github.com/user-attachments/assets/7dcab25d-8cb2-476d-873b-7aff2aebfd53)
### Pivot Table - Microsoft Excel
![Screenshot (88)](https://github.com/user-attachments/assets/38e0be11-66d3-43a6-b904-964c19a8f786)
### Pie Chart - Microsoft Excel
![Screenshot (144)](https://github.com/user-attachments/assets/3c3df258-dc06-4988-b97d-e4ebbc634231)
### Filtered Column Chart for 2023
![Screenshot (148)](https://github.com/user-attachments/assets/09f653f0-e452-4140-aa81-f8432b06c779)
### Filtered Column Chart for 2024
![Screenshot (147)](https://github.com/user-attachments/assets/78d9a11e-bd57-4245-97df-c91aae35fc25)

### i. Data Overview
- Basic Subscription is a low-cost plan with limited features.
- Standard Subscription is a mid-tier plan offering moderate features.
- Premium Subscription isa high-cost plan with premium features and services.

### ii. Inferences
- #### Revenue Concentration;
   * According to the pie chart, Basic subscription makes up 50.01% of total revenue. The rest of the 50% is generated by both the Standard and Premium Subcriptions. This indicates that larger volume of customers go for affordable plans over features.
- #### Customer Resistence to Higher Subscription Type;
   * The lower revenue contribution from Standard and Premium Subscriptions suggests that customers may not perceive enough value to want to upgrade.
### iii. Strategic Recomendations
 - Petal should enhance perceived value of Standard and Premium plans by adding exclusive features e.g bundled services or faster network speed.
 - Educate Basic Subscription users on the benefits of Standard and Premium Subscriptions through targeted campaigns and also review their prices and make it competitive without affecting potential profits on upgrades. 
### iv. Conclusion
- By enhancing percived value and upgrading the service, Petal can balance its revenue distribution well and increase profitability. Their goal is to reduce customer dependency on Basic Subscription making upgrades appealing and affordable in a way that alings with customer expectations.

## 4. Total number of Active and Cancelled Subscription - SQL
## Active Subscription 
![Screenshot (113)](https://github.com/user-attachments/assets/3b512405-95fe-4f09-b7f1-61e3381c3300)

## Cancelled Subscription 
![Screenshot (114)](https://github.com/user-attachments/assets/7c61534c-7817-4783-948c-599f2a93eb62)

### i. Data Overview
- Active subscribtion represents the number of customers currently subscribed to the internet service.
- Canceled subscription refers to the number of customers who canceled their subscription and left the service.
### ii. Customers satisfaction and Service quality
- The returns om the SQL queries show that the no. of customers who are currently subscribed are more than the customers that left which may suggest that the service is of good quality.
- Even though the returns show that active is more than canceled subscription, the number of subcribers that canceled are quite much which may indicate poor network performance, rising competition or inadequate customer support.
### iii. Strategic Recommendations
For Petal Internet Service to manange the active and canceled subscriptions effectively, they can implement the following strategies.
- Ratain existing customers by enhancing service quality focusing on improving network reliability and speed, and also offering discounts or package upgrades to long-term subscribers.
- They can minimize new cancellations by gathering regular feedback from customers, especially those who cancel their subscription, which will provide insights to address common concerns. Petal should ensure pricing is competitive by benchmarking against other providers in the market.
### iv. Conclusion 
- By understanding the factors behind active and cancelled subscriptions, Petal Internet Service Provider can drive improvements across engagement and pricing strategies.
- The strategic recommendations mentioned above will likely lead to higher retention rates and having a number of customers who are satisfied with the service.


## 5. The most popular Subscription Type by the number of Customers
![Screenshot (109)](https://github.com/user-attachments/assets/5f1505b7-5a25-4735-99e3-58c02776f953)
### i. Data Overview
-  Out of 33,787 customers, 16,921 customers are subscribed with the Basic Subscription plan making Basic plan the most popular subscription type.
### ii. Inferences
- #### Affordability;
  * The high popularity of basic subscription could suggest price-sensitive cusstomers who go for cheap andaffordable prices.
- #### Service Requirement;
  * Many customers may only need the internet for basic tasks leading them to settle for theleast plan.
### iii. Strategive Recomendations
- Petal should introduce targeted marketing campaigns to encourage basic subscribers to upgrade to a standard or the premium plan.
- They should consider introducing a "Basic+" plan with a price slightly higher than that of the Basic Subcription and offers more features than the basic plan to imporve in revenue generated.
### iv. Conclusion
- The popuarity of the Basic Subscription plan highlights a significant market segment that values affordability. Therefore, to maximize revenue, the above strategic recomendations can be implemented to help shift some basi subscribers to higher plans.
  
## 6. Customers who cancelled their Subscription within 6 months
![Screenshot (103)](https://github.com/user-attachments/assets/6a4ab5b8-2381-4657-b5d9-eaa92023ba88)
### i. Overview Analysis
- A zero cancellation rate within six months is a retention indicator which may sugest that customers are satisfied with the services.
### ii. Inferences
- #### Trial or Temporary Use;
  * Some customers might subscribe for a year because they want to assess the performance of the provider service over a longertimeframe.
- #### Yearly Pricing Discounts'
  * Customers might have subscriped because Petal internet service offers discounts incentives for customers that subscribes for more than six months. This also provides the customers a way to experience the service and see if it suits their preferences.
### iii. Strategic Recomendations
- To prevent cancellations, the internet service provider should try to identify and adress any minor issues customers may face by conducting a survey.
- Regulary benchmark against market pricing so as to ensure that competitors don't lure their customers away with competitive pricing.
### iv. Conclusion
A zero cancellation rate in the first six monts reflects positively on Petal's service quality, pricing strategy and customer experience. By actively gathering feedback from the customers and offering discounts and promotions, Petal Internet Service Provider can retain customers.


## 7. Average Subscription Duration for all Customers
## SQL Query 
![Screenshot (104)](https://github.com/user-attachments/assets/4a3eb551-07ec-42da-8a28-763c1119f44e)
### i. Inferences
- #### Custormer Loyalty:
A one year average subscription duration suggests that customers tend to stay for a long period. This may indicate a strong product market.
- #### Competitive Positioning:
Customers subscribing for a year might suggest that they see high quality service indicating that it provides long-term benefits rather than short-term appeal.
### ii. Strategic Recommendations
- Petal Internet service Provider can ntroduce options for longer subscription duration e.g two years at discounted rates to encourage longer commitments.
- To maintain or increase to subscription duration years, PISP should ensure continuous infrastructure and features upgrades to optimize internet speed.
- They can also consider providing semi-annual and quarterly renewal duration options to attract low budget customers allowing them to commit for shorter duration then upgrade to the annual later.
### iii. Conclusion
- With an average subcription of 365 days, PISP demonstrates solid customer rentation. To sustain and extend this average, they should focus on improving service reliability, introducing flexible prices andimplementing the recomendations stated above so as to enhance customer satisfaction and have long-term subscribers. 


## 8. Custormers with Subscription longer than 12 months
![Screenshot (112)](https://github.com/user-attachments/assets/cb96ccfa-66e4-4cb8-818a-476be8c7bfe8)
### i. Inferences
- #### Low Satisfaction or Value Perception;
  * Custormers may not see enough value in the service to maintain long-term subscription. This could be due to poor custormer support or service reliability problems.
- ### Trial or Temporary Use Cases;
  * Some customers for have subscribed for short-term needs.
- Competitors may offer more appealing packages at lower prices than Petal hence causing customers to switch providers within a year.
### ii. Strategic Recommendations
- Petal should conduct surveys to understand why customers are leaving and not renewing.
- They should improve their service quality inorder to improve on customer satisfaction.
- They can also offer discounts for renewals for those who go for long-term plans.
### iii. Conclusion
Not having customers that subscribe for more than a year means that customers are not finding enough value to subscrip to that service for a long-term. Adressing and implementing the Strategic recomendations pointed out above will help foster longer subscription durations and build costomer loyalty.

## Customer Data Visualization Dashboard for Petal Internet Services

## Filterd Dashboard for the year 2023
![Screenshot (130)](https://github.com/user-attachments/assets/4730c02e-d578-4712-9f72-a400d96ab552)
## Filterd Dashboard for the year 2024
![Screenshot (129)](https://github.com/user-attachments/assets/d8c09704-32a2-4b74-8741-8e548c76cff3)
![Screenshot (131)](https://github.com/user-attachments/assets/56fc1ecd-a33b-42c3-abe8-6994dce76fe5)



