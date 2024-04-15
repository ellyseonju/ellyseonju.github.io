---
layout: single
title: "[PowerBI] All Access Churn Analysis Dashboard"
categories: BI
tag: PowerBI
---

![PowerBI Dashboard Picture_Update](https://github.com/ellyseonju/ellyseonju/assets/142702152/8c9812d8-2984-4a21-a457-aaa31e1a2a83)

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
    * Run SQL in Snowflake
        ```ruby
        SELECT ACTIVE_USER_MEMBERSHIPS.customer_uuid, RESERVATIONS.location_name, CUSTOMERS_PII_PERSONAL.gender, CUSTOMERS_PII_PERSONAL.date_of_birth, CHURN_MONTHLY.tenure_in_months, ACTIVE_USER_MEMBERSHIPS.product_name, RESERVABLE_MONTHLY.is_occupied, DATE(ACTIVE_USER_MEMBERSHIPS._run_at) AS date_only
        FROM CENTRAL.CDM_WORKSPACE_ACCESS.ACTIVE_USER_MEMBERSHIPS
        LEFT JOIN CENTRAL.CDM_CUSTOMERS_PII_PERSONAL.CUSTOMERS_PII_PERSONAL
        ON ACTIVE_USER_MEMBERSHIPS.CUSTOMER_UUID = CUSTOMERS_PII_PERSONAL.CUSTOMER_UUID
        LEFT JOIN CENTRAL.CDM.RESERVATIONS
        ON ACTIVE_USER_MEMBERSHIPS.ACCOUNT_UUID = RESERVATIONS.ACCOUNT_UUID
        LEFT JOIN CENTRAL.CDM_REPORTING.CHURN_MONTHLY
        ON ACTIVE_USER_MEMBERSHIPS.ACCOUNT_UUID = CHURN_MONTHLY.ACCOUNT_UUID
        LEFT JOIN CENTRAL.CDM_FEATURE_STORE.RESERVABLE_MONTHLY
        ON ACTIVE_USER_MEMBERSHIPS.ACCOUNT_UUID = RESERVABLE_MONTHLY.ACCOUNT_UUID
        WHERE date_only BETWEEN '2023-01-01' AND '2024-04-03'
        ```
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
    * Churn Rate and Customer Trends by Age grouping 
       
        ![Churn_age grouping_update](https://github.com/ellyseonju/ellyseonju/assets/142702152/29d39942-d66e-4a5f-b953-d9267d095b4f)
        * The number of Customers and Customers Lost for each age group are as follows!
            * < 20: 6 / 100 (6%)
            * 21 ~ 30: 168 / 2,247 (7.5%)
            * 31 ~ 40: 645 / 5,270 (12.2%)
            * 41 ~ 50: 946 / 2,771 (34.1%)
            * 51 ~ 60: 522 / 942 (55.4%)
            * 61 ~ 70: 124 / 397 (31.2%)
            * over 71: 12 / 151 (7.9%)
        
        As you cans see, the highest churn rate is in 51 ~ 60. Slightly it looks like pain point but the proportion of that age group to the total number of customers accounts for about 12%.
        On the other hand, 31 ~ 40s, which accounts for the most of all customers, is 12% showing a healthy turn rate. Next, those in their 41 ~ 50s with the largest customer base show a rather high turn rate of 34.1%.
    * Churn Rate and Customer Trends by district

        ![Churn_district_update 2](https://github.com/ellyseonju/ellyseonju/assets/142702152/b7567ba9-b662-4c4b-8358-7cf06f22f032)
        * In the WeWork Building Area, buildings in the YBD area show a high turn rate (21.2%). Looking more closely- YBD had a high churn rate in 31 ~ 40s. It can be interpreted as a building group that is not preferred by that age group.
        ![Churn_District_detail](https://github.com/ellyseonju/ellyseonju/assets/142702152/3031c90b-645d-48a0-bae0-58e383bc3347)
    * Churn Rate and Customer Trends by tenure
       
        ![Churn_tenure_update 2](https://github.com/ellyseonju/ellyseonju/assets/142702152/ff6d6c79-fade-438d-9433-b6c06cb35a46)
        * Customers who have been in use for less than a year have the highest churn rate (22.6%). However, it is not a meaningful analysis because the total number of customers is small. If It approach  more analytically, the customer's dropout rate increases in the 1 ~ 3rd year of use, and the churn  rate decreases in the long-term user period of 7 ~ 9 years.

* Recommendations to reduce customer churn rate
    * 