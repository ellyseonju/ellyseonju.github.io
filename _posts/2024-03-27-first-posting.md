---
layout: single
title: "[PowerBI] All Access Churn Analysis Dashboard"
categories: BI
tag: PowerBI
---

![PowerBI Dashboard Picture 2](https://github.com/ellyseonju/ellyseonju/assets/142702152/e41ff381-a4b0-4f5c-ba75-d1072ce37a7a)

## Overall 
* Audience: Sales Team 
* Purpose
    * Analyze customer churn patterns from various angles to identify customer behavior by finding groups with high churn rates. (This project uses data such as customer gender, tenure, district, age information to identify trends in customer churn and identify strategies for reducing it.)
* Consider answering the following questions
    * 
* Raw Data
    * The data used on the dashboard is composed of dummy data according to the company data protection policy
    * Datasets
        - customer_id
        - district
        - gender
        - age
        - tenure
        - products_type: 1, 2
        - active_member: 1, 0
        - churn: 1, 0 

## Data Preparation & DAX
* Change Data Type 
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
