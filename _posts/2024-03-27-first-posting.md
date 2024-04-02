---
layout: single
title: "[PowerBI] All Access Churn Analysis Dashboard"
categories: BI
tag: PowerBI
---

![PowerBI Dashboard Picture 2](https://github.com/ellyseonju/ellyseonju/assets/142702152/e41ff381-a4b0-4f5c-ba75-d1072ce37a7a)

## Overall 
* Target department: Sales Team 
* Business Situation
    * With the recent increase in customer churn rates using all access, the sales team have tasked me with analyzing customer churn patterns from various angles to identify customer behavior by finding groups with high churn rates. They've asked me to extract data such as customer gender, tenure, district, age information to identify trends in customer churn and identify strategies for reducing it
* Consider answering the following questions to prepare data 
    * Is there specific tenure section with the highest  churn rate?
    * Is there a correlation between the churn rate and the WeWork building Distirct? 
    * Which product has the highest churn rate 
    * Which age group has the lowest churn rate and which product do they prefer
* Tools Used for data: Snowflake, SQL, PowerBI, Excel
* Extract Data 
    * Run SQL in Snowflake -> 구문 넣기 
    * Data Structure
        - customer_id
        - district
        - gender
        - age
        - tenure
        - products_type: 1, 2
        - active_member: 1, 0
        - churn: 1, 0

## Data Preparation & DAX
* Change Data Type: Converted ‘tenure’ column from string to number format. Removed trailing spaces in name of each column
* Transform Data
    * Replace Values
        - products_type: 1(Plus), 2(Basic)
        ![Replace Value](https://github.com/ellyseonju/ellyseonju/assets/142702152/754c4a7b-6f9a-49d7-9db2-47038ea4bcba)

        - active_member: 1(active), 0(Inactive)
        ![Replace Value 2](https://github.com/ellyseonju/ellyseonju/assets/142702152/28efc295-bb70-489f-ade2-dbfc12bdc739)

        - churn: 1(Churned), 0(Not churned)
        ![Replace Value 3](https://github.com/ellyseonju/ellyseonju/assets/142702152/c79a1545-4ec6-478b-9449-6e8ad4cdca93)
    * Conditional Column
        - Age Grouping: Ease of identifying age groups where churn rate is high & getting the research team to do a focussed study on specific age groups
        ![Conditional Column](https://github.com/ellyseonju/ellyseonju/assets/142702152/e2f48492-73bb-4cca-a5c3-46f71be5603e)

        - Tenure Grouping: Grouping the tenure to identify which section has a high churn rate
        ![Conditional Column 3](https://github.com/ellyseonju/ellyseonju/assets/142702152/9a0bb4d0-88a2-4124-9aef-047ab8649140)

* DAX: mainly use theree DAX for this dashboard 
    * Number of customers
    ```ruby
    Customers = COUNT('All Access Raw Data'[Customer])
    ```
    * Number of customers lost
    ```ruby
    Customers Lost = CALCULATE( COUNT('All Access Raw Data'[Churn Status]), 'All Access Raw Data'[Churn Status] = "Churned")
    ```
    * Churn Rate (%)
     ```ruby
    Churn Rate = 'All Access Raw Data'[Customers Lost]/'All Access Raw Data'[Customers]
    ```
    
    
## Conclusion
* Insight Section
* Recommendations to reduce customer churn rate
