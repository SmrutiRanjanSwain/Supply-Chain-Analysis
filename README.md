# Supply-Chain-Analysis
##  Executive Summary
This report presents a comprehensive analysis of the delivery operations of a global e-commerce company managing end-to-end order fulfillment across multiple regions. The analysis covers 172,765 orders spanning
January 2015 through January 2018, focusing on identifying root causes of chronic late deliveries, quantifying their financial impact, and establishing a data-driven framework for improvement.




The headline finding is stark: 54.71% of all orders are delivered late, 
costing the business $2.1M in eroded profitability on delayed orders alone. 
While total profit across fulfilled orders reached $7.5M, 
the persistent late-delivery problem represents both a significant financial drain and a major customer experience risk. 
A Random Forest predictive model achieved 74% accuracy in identifying at-risk orders before they become late.

<img width="847" height="200" alt="image" src="https://github.com/user-attachments/assets/00334b59-db8c-44df-a057-7783845fb96b" />

## Business Context & Objectives
The company operates a global e-commerce platform selling products across categories including sporting
goods, fitness equipment, outdoor gear, footwear, and apparel across multiple international regions.

### Core Business Problem
Actual shipping times frequently deviate from scheduled delivery windows, creating eroded customer trust,
reduced order profitability, and an inability to make reliable commitments to buyers at point of purchase.

### Analytical Objectives
 * Understand the current state of delivery performance across all dimensions (region, mode, time, segment)
 * Quantify the financial impact of delays on order profitability
 * Identify the primary operational bottlenecks driving late deliveries
 * Build a predictive model to flag high-risk orders before they are shipped
 * Deliver actionable recommendations to improve on-time delivery and profitability

## Key Performance Indicators (KPIs)
The following KPIs were computed directly from the cleaned dataset to establish a performance baseline.

* Total Orders- 172,765                        
* Late Deliveries- 94,523
* Late Delivery%- 54.71%
* On-Time Delivery%- 45.29%
* Total Profit (profitable orders)- $7.5M
* Profit at Risk (delayed orders) $2.1M
* 90th Percentile Delay 3 days
* Avg Order Profit $22.03

### Late Delivery Rate at 54.71%
More than half of all orders arrive late. This is not an edge-case problem - it is the default experience for the majority of customers.

### $2.1M Profit at Risk
Orders that experienced delays collectively generated $2.1M in profit that is under constant pressure from further operational deterioration.

### 90th Percentile Delay = 3 Days
Even the most extreme cases are contained within 3 days of lateness, suggesting the problem is systemic and process-driven rather than catastrophic.

## Profitability Analysis
### 4.1 Profitability Distribution
Order-level profitability was classified into three tiers based on Order Profit Per Order. While 80.7% of orders
are profitable, the 18.7% loss-making share represents a meaningful drag that is disproportionately
concentrated among delayed shipments.


<img width="439" height="410" alt="image" src="https://github.com/user-attachments/assets/396254e8-24a9-4342-bd3a-03237bc00dab" />

Figure 1: Profitability Distribution
### 4.2 Delay Distribution & Profit vs. Delay Days
The delay distribution shows that 31.0% of all orders alrive exactly 1 day late the single largest cohort.
Combined, orders delayed by 1-4 days account for 54.7% of all order volume, directly mapping to the overall
late delivery rate.

<img width="1347" height="536" alt="image" src="https://github.com/user-attachments/assets/ff5379fc-7b59-4504-89aa-94c2f159e9ba" />

Figure 2: Delay Distribution (left) and Profit Analysis by Delay Days (right)

#### A critical observation:

Mean profit per order remains stable at approximately $21-$23 across all delay levels.
The profitability problem is therefore driven by volume of delayed orders, 
not by individual order economics making systemic throughput improvement the highest-leverage intervention.

## Bottleneck Detection

Delay percentage was computed across six key operational dimensions. The charts below reveal where the fulfillment process breaks down most severely.
<img width="1611" height="711" alt="image" src="https://github.com/user-attachments/assets/f1289e72-dde4-409b-a1ba-4e21ae416fea" />
Figure 3: Delay % across six operational categories- Region, Segment, Shipping Mode, Order Status, Payment Type,
Department
### Shipping Mode is the #1 Lever
First Class: 100% delay rate. Second Class: 79.8%. Standard Class: 39.8%. Same
Day: 0%. The mode assignment logic is the most impactful single variable to fix.

### Regional Spread is Narrow (55-59%)
Central Africa leads at 58.7% but all regions cluster between 55-59%. This rules out a localised logistics failure and confirms a company-wide systemic issue.

### Customer Segments Nearly Identical(54.5-55.4%)
No segment receives preferential service. All customers - Consumer, Corporate,
Home Office - experience the same broken delivery promise.

### Health & Beauty (56.9%) and Pet Shop (56.6%) Lead by Department
These departments marginally outpace others in delay rate, warranting an inventory and carrier audit for these product categories.

## Root Cause Analysis

Central Africa was selected for deep-dive root cause analysis as the highest-delay region (58.7%). The chart
below ranks the top 10 driver factors by delay percentage within this region.
<img width="764" height="444" alt="image" src="https://github.com/user-attachments/assets/1580ad66-d5c8-4c04-aa46-ef1f093c50a8" />

Figure 4: Top 10 Drivers of Late Delivery in Central Africa - ranked by delay percentage
## Time-Based Delay Patterns
Three temporal dimensions were analysed: month of year, day of week, and hour of day. While delay rates are relatively stable across all dimensions (53-57%), specific peaks highlight opportunities for targeted
capacity planning.
<img width="1790" height="590" alt="image" src="https://github.com/user-attachments/assets/02ff8d5b-50c2-4707-bd6e-07ecf8d648b2" />

Figure 5: Delay % by Month (left), Day of Week (centre), and Hour of Day (right) - red annotations mark the top 3 peaks in
each dimension

### Peak Delay Months:August & September (55.4%) and December (55.2%)
August and September are the highest months at 55.4%, with December close behind. These reflect mid-year promotions and Q4 holiday surge overwhelming fulfilment capacity. July represents a notable low-point (~53.75%), confirming seasonal variation is plannable.

### Day-of-Week Variance is Minimal
Monday (55.5%) and Sunday (55.2%) are the peak days, but the spread across the week is less than 1 percentage point. Day-of-week is not a meaningful lever for operational intervention.

### Intra-Day Peaks: Hour 21 (57.1%), Hour 11 (56.7%), Hour 12 (56.0%)
Late-evening orders (hour 21) have the highest delay rate at 57.1%, likely reflecting processing cutoff windows. Midday peaks suggest bottlenecks during peak-volume hours.

## Machine Learning Model Results
A supervised classification model was built to predict whether an individual order will be delivered late (Late_delivery_risk = 1). 
The pipeline included frequency encoding of categorical variables, stratified
train/test split, SMOTE oversampling to address class imbalance, and Random Forest classification.

<img width="643" height="177" alt="image" src="https://github.com/user-attachments/assets/b6780d38-c266-4a45-9308-77a59219de16" />

<img width="634" height="225" alt="image" src="https://github.com/user-attachments/assets/177e6f46-9f7b-4a59-98df-7766e775201b" />

### 74% Overall Accuracy
The model correctly classifies nearly 3 in 4 orders - a strong foundation for production deployment as an order-level late-delivery alert system.

### Higher Precision on Late Orders (0.78)
When the model predicts an order will be late, it is correct 78% of the time - sufficient to trigger targeted interventions without generating excessive false alarms.

### Recall for Late Orders at 0.75
The model captures 75% of actual late orders. The 25% miss rate is acceptable for a first-generation alert system, with clear improvement potential.

### Class 0 Harder to Predict (Precision 0.68)
On-time deliveries share many characteristics with late ones given the systemic nature of delays, making them genuinely difficult to distinguish.

## Strategic Recommendations
Based on the findings across all analytical dimensions, the following prioritised actions are recommended:

### CRITICAL
1. Immediately Audit First Class & Second Class Shipping Capacity
First Class shipping has a 100% delay rate and Second Class 79.8%. These modes operate in
complete contradiction to their brand promise. Conduct an immediate carrier SLA audit. Until
resolved, consider suspending First Class or repricing to reflect actual performance.

### HIGH
2. Deploy the Predictive Alert System
The Random Forest model (74% accuracy, 78% precision on late orders) is ready for production
piloting. Integrate it into the order management system to flag high-risk orders at confirmation and
trigger proactive customer communication and priority handling queues.

### HIGH
3. Resolve Payment Processing Bottlenecks
Orders in FAYMENT_REVIEW (55.3% overall; 80.0% in Central Africa) and PENDING_PAYMENT
(55.0%) have significantly elevated delay rates. Introduce automated escalation for stalled payment reviews exceeding 2 hours.

### MEDIUM
4. Develop Seasonal Surge Capacity Plans
August, October (55.4%), and December (55.2%) are peak delay months. Build pre-season capacity plans including temporary logistics partnerships, inventory pre-positioning, and adjusted
delivery promise windows.

### MEDIUM
5. Default to Standard Class for Eligible Orders
Standard Class achieves a 39.8% delay rate - far superior to First and Second Class.
Re-evaluate shipping mode assignment logic to default eligible orders to Standard Class,
particularly in regions and departments with poor premium mode performance.

### MEDIUM
6. Investigate High-Delay Departments in Africa
Outdoors (61.3%) and Golf (60.8%) in Central Africa show significantly elevated delay rates.
Conduct a warehouse-level audit of stock availability, pick-and-pack times, and carrier assignment
for these product categories.

### LOW
7. Reduce Loss-Making Order Share (18.7%)
The 18.7% loss-making order share warrants a separate pricing and discount review. Combine with
delay analysis to identify whether discounted orders are disproportionately late, creating a
compounded margin problem.

### LOW
8. Continuously Retrain the Predictive Model
Retrain the model quarterly. Explore adding carrier-level data, weather events, and warehouse utilization features. Target a recall improvement to above 80% on late orders within 6 months.

## Conclusion
This analysis has surfaced a clear and urgent picture: a global e-commerce operation where the majority of
orders (54.71%) fail to meet their promised delivery windows, costing $2.1M in at-risk profit and undermining
customer trust at scale.
The root causes are identifiable and addressable. Shipping mode misconfiguration (First Class at 100% late,
Second Class at 79.8%) is the dominant operational failure. Payment processing friction creates a secondary
bottleneck. Seasonal volume spikes are not adequately planned for. And geographic disparities, while
present, are secondary to the systemic company-wide pattern.
A Random Forest predictive model trained on readily available order features already achieves 74%
accuracy in identifying at-risk orders. This is a deployable tool, not a future aspiration.

<img width="633" height="222" alt="image" src="https://github.com/user-attachments/assets/aac18201-1c21-41d7-b7e3-de0c70e4687e" />


With focused execution on the eight recommendations in this report starting with the critical shipping mode
audit and predictive alert system deployment the business can systematically recover its delivery
performance, protect its $7.5M profit base, and build the operational reliability that sustained e-commerce
growth demands.


