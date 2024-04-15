---
layout: single
title: "[Tableau] Building Performance Report"
categories: BI
tag: Tableau
---
![PART 1](https://github.com/ellyseonju/ellyseonju/assets/142702152/97dc467c-0bf2-4cd5-9479-3e4fcb741092)

## Overall 
* Target Audience: General Manager, Strategy Team, Sales Team 
* Dashboard Purpose
    * Operational & Tactical: This dashboard is engineered to monitor detailed measuring data variables in relation to time (week, month,year, etc.). An example would be to conduct an analysis of Occupancy (%), NARPM, Commitment Term, Office Inventory Count over a designated period to monitor the overall health of buildings. They offer a great deal of insight into weekly trends and metrics and are pivotal in improving internal communication and formulating mid to long-term strategies across departments from sales and strategy right the way through to general manager.
* Key Metrics using in this dashboard
    * Office SKU: Divided the office SKU according to the number of desks 
        * SKU Bucket: 1-9p, 10-49p, 50-99p, 100-149p, etc 
        * SKU Bucket Detail
            * 10-49p: 10-14p/ 15-19p/ 20-24p.. etc 
    * Occupancy %
        * Calculation: sum([Occupancy (Desks)])/sum([Capacity (Desks)]) 
    * Win Rate %
        * Calculation: sum([Is Won Opportunity (Dim Sf Opportunity1)])/sum([Is Closed Opportunity (Dim Sf Opportunity1)])
    * NARPM: Net Average Revenue per Member 
    * Commitment Term: Contract period (month) 
    * Office Inventory Count (%): Percentage of offices in specific SKU out of the total number of offices
        * Special note: This was added to prevent the status of office holdings concentrated on a specific SKU

## Dashboard Design
* Intro: This dashboard consists of several tabs according to the needs of the audiences 
* Design 
    * Tap 1: Building Healthy Overview 
        * Target Audience: General Manager & Strategy 
        * Purpose: Track of trends in one place. By compiling trend information visually, I wanted to give them a quick view to see the overall health of buildings in different areas and to quickly take actions. 
        * 3 main visualizations: Design that gradually breaks down in detail 
            - Overview by SKU (Focused on Various months) 
            ![PART 1](https://github.com/ellyseonju/ellyseonju/assets/142702152/c077008a-bcf3-4160-903e-f41675779fac)
                - Description: Metrics according to 4 types (Occupancy %, NARPM, Commitment Term, Office Inventory Count %) can be checked by building and date in Last 6 months 
            - Building Descending 
            ![PART 3](https://github.com/ellyseonju/ellyseonju/assets/142702152/6f1a0313-bda1-483e-b32a-ff6fe47088c0)
                - Description: This is more building specific view not overall. List up the numbers of 19 WeWork buildings in descending order by 4 types
            - Mix Chart 
            ![PART 4](https://github.com/ellyseonju/ellyseonju/assets/142702152/6b906378-33c7-4200-b9e0-116b2c28ebad)
                - Description: Through the line chart, the correlation between commitment Term, NARPM, and Occupancy % can be identified. Click on a specific point to see the corresponding account details

    * Tap 2: Building Comparison 
        * Target Audience: Sales Team 
        * Purpose: This tab can check the numeric gap between buildings according to Office SKU by focusing on various buildings. For example, the stakeholders can compare the buildings with the highest and lowest for 10p office occupancy at once so that when they set up a sales strategy, it is a good insight into where to focus 
        * 3 main visualizations 
            - Comparative Building Analysis (Focused on various buildings)  
            ![PART 6](https://github.com/ellyseonju/ellyseonju/assets/142702152/d823f84c-35bc-401c-ad88-19eedd735374)
                - Description: Unlike being able to see a historical trend based on one building, this visualization can compare several buildings immediately. Depending on the metric type you want to see, it is possible to compare by building with office distribution according to SKU, occupancy %, etc
            - Comparative Building Analysis (detailed SKU) 
            ![PART 7](https://github.com/ellyseonju/ellyseonju/assets/142702152/e1bd4546-0f64-4f6d-b4f6-4a86d633743a)
                - Description: The same format as the Comparative Building Analysis, but the SKU bucket is listed into a single SKU in more detail. 
            - Comparative Building Analysis (Win rate %) 
            ![PART 8](https://github.com/ellyseonju/ellyseonju/assets/142702152/772eb5e6-9294-4b2a-aad9-b8448901882e) 
                - Description: You can check the win-rate among closed sf opportunities. Similar to other visualizations, 1) you can see historical data based on one building, or 2) you can compare win rates around multiple buildings

## Reference 
You can check out the real dashboard via my [Tableau Public](https://public.tableau.com/app/profile/elly.jin/vizzes!)! The design is same, but the data is dummy one with the company's data protection policy. 
    
