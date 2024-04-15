---
layout: single
title: "[Tableau] Community Manager Operations Dashboard"
categories: BI
tag: Tableau
---
![PART 1](https://github.com/ellyseonju/ellyseonju/assets/142702152/65d5c277-f504-4655-8b83-a3c59dda960b)
## Overall
* Target Audience: Community Manager 
* Dashboard Purpose
    * Monitor Building Healthy: Deploying occupancy analytics that can help detect the maximum number of member in an area; and set up the strategy for utilizing office spaces 
    * Manage Account: Check out the Conference Room Utilization Rate, occupied desks, and service revenue for a particular account
    * Proactive Check-in Status (KPI tracking): Displays completion rate in interactive charts and graphs, allowing for quick, organized review and preparation for proactive check-in through upcoming list
    * Track Ancillary Revenue: Analyzing the Ancillary Revenue Trend to identify the weakness category to achieve the business goal, and make a plan to promote 
* Key Metrics using in this dashboard
    * Occupancy %
        * Calculation: sum([Occupancy (Desks)])/sum([Capacity (Desks)])
    * Utilization Rate % 
        * SUM([Hours])/198 
            * 198: 9 hours a day on weekdays 22 days a month 
    * NARPM: Net Average Revenue per Member 
* Technical Skills using in Tableau 
    * Calculated Field 	
        * Mainly use IF function  

## Dashboard Design
* Intro
    * This dashboard consists of several tabs which is mainly needed for building management 
* Design 
    * Tap 1: Building General (Occupancy & Account) 
        * Building Occupancy (%) – by floor
        * Building Occupancy (%) – by Office SKU
        * Building Account NARPM – by SKU
        * The number of Accounts by SKU 
    * Tap 2: Account Directory (dedicated to specific account information by account filter) 
        * Price Information (Desk occupied, ARPM) 
        * Proactive Check-in Status 
        * Conference Room Utilization % 
        * Conference Room Utilization % - Detail 
        * Service Revenue Status 
        * Service Revenue Detail 
    * Tap 3: Proactive Check-in Status 
        * Proactive Check-in Status 
        * Proactive Check-in (Detail) 
        * Proactive Check-in (Upcoming) 
    * Tap 4: Conference Room Utilization % 
        * Conference Room Inventory by SKU
        * Utilization Rate (%) 
    * Tap 5: Service Revenue Status 
        * Service Revenue Trend 
        * Service Revenue by category 
        * Service Revenue Detail 

## Reference 
You can check out the real dashboard via my [Tableau Public](https://public.tableau.com/app/profile/elly.jin/vizzes!)! The design is same, but the data is dummy one with the company's data protection policy
