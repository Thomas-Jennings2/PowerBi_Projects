# Databel Customer Churn Analysis
<img width="1324" height="744" alt="image" src="https://github.com/user-attachments/assets/35611f1d-c743-490b-b6ec-2bec8a53911c" />

## Importing The Data

The data used in this project was from a fictional company called Databel provided by Datacamp. This dataset was imported into Power BI for analysis of customer churn, demographics, contracts, customer service and additional charges.

---

# Data Exploration

## Customer Measures

Two measures were created to investigate the number of customers in the dataset.

### Number of Customers

Number of Customers = COUNT('Databel - Data'[Customer ID])


### Unique Customers

Unique Customers = DISTINCTCOUNT('Databel - Data'[Customer ID])


Two cards were created to compare the results of these measures.

Both measures returned the same result, indicating that each customer ID appears only once in the dataset.

---

# Calculating Churn

A new column called `Churned` was created to convert the `Churn Label` values from "Yes"/"No" into binary values.

- Yes = 1
- No = 0

### Churned

Churned = IF( 'Databel - Data'[Churn Label] = "Yes", 1, 0 )


### Number of Churned Customers

Number of Churned Customers = SUM('Databel - Data'[Churned])


### Churn Rate

Churn Rate = DIVIDE( SUM('Databel - Data'[Churned]), COUNTROWS('Databel - Data'), 0 )


---

# Visualise Churn Reasons

A bar chart was created using:

- **Number of Customers**
- **Churn Reason**

This was used to identify the most common reasons customers leave Databel.

The analysis was then used to identify the **top three churn reasons**.

<img width="918" height="592" alt="image" src="https://github.com/user-attachments/assets/4f3a9aef-f0d2-4ce5-80c6-d44077564a75" />

---

# Churn Reason by Category

A visual was created using:

- **Churn Category**
- **Churned**
- **Percentage of total values**

This allows churn reasons to be analysed at a broader category level.

---

# Churn Rate by State

A map visual was created to investigate differences in churn rates across states.

The following measures were added to the tooltip:

- Churn Rate
- Number of Customers
- Number of Churned Customers

`State` was added to the map and conditional formatting was used to highlight states with higher churn rates.

---

# Analyse Demographics

## Demographic Groups

A demographic column was initially created using age:

Demographics = IF( 'Databel - Data'[Age] >= 30, "Senior", IF( 'Databel - Data'[Age] < 30, "Under 30", "Other" ) )


However, this did not produce the expected results.

After inspecting the dataset, two existing Boolean-style columns were discovered:

- `Senior`
- `Under 30`

The demographic calculation was therefore changed to:

Demographics = IF( 'Databel - Data'[Senior] = "Yes", "Senior", IF( 'Databel - Data'[Under 30] = "Yes", "Under 30", "Other" ) )


This produced the expected demographic groups.

---

## Churn Rate by Demographic

A bar chart was created showing churn rate by demographic group.

The analysis showed that **senior customers had the highest churn rate**.

---

# Age Bins

Age bins were created using Power BI's grouping functionality.

- Right-click `Age`
- Select **New Group**
- Set the bin size to **5 years**

A line and stacked column chart was then created showing:

- Number of Customers
- Churn Rate
- Age Bins

---

# Investigating Customer Groups

The `Monthly Charge` column was changed to currency format.

A bar chart was created showing the average monthly charge by customer group.

A stacked column and line chart was also created to compare:

- Number of Customers
- Monthly Charge
- Churn Rate

---

# Contract Analysis

A new column called `Contract Category` was created to group one-year and two-year contracts together.

### Contract Category

Contract Category = SWITCH( 'Databel - Data'[Contract Type], "One Year", "Yearly", "Two Year", "Yearly", "Monthly" )


A multi-card visual was created to compare churn rates between:

- Monthly contracts
- Yearly contracts

A clustered bar chart was also created to compare churn rate by:

- Contract Type
- Gender

---

# Unlimited Data Plan

The effect of unlimited data plans on churn was investigated.

A new column called `Grouped Consumption` was created to classify customers based on their average monthly GB download.

The groups were:

- Less than 5 GB
- Between 5 and 10 GB
- 10 or more GB

### Grouped Consumption

Grouped Consumption = IF( 'Databel - Data'[Avg Monthly GB Download] < 5, "Less than 5 GB", IF( 'Databel - Data'[Avg Monthly GB Download] < 10, "Between 5 and 10 GB", "10 or more GB" ) )


A clustered bar chart was created to compare churn rate by:

- Unlimited Data Plan
- Grouped Consumption

---

# International Plan

A matrix was created using:

- **International Plan** as columns
- **International Active** as rows
- **Churn Rate** as values

The visual was also filtered by state.

One notable finding was that **72% of customers in California who make international calls but do not have an international plan churned**.

This could indicate an opportunity to review whether these customers are on suitable plans and whether alternative plans could improve retention.

---

# Customer Service

Three areas were investigated:

- Payment method
- Contract type
- Customer tenure

A line chart was created using account length and churn rate to investigate whether churn decreases as customers remain with Databel for longer.

A bar chart was also created to show the number of customers by payment method.

---

# Final Dashboard

The Power BI canvas was configured to:

- Width: **1640px**
- Height: **960px**

The main dashboard includes:

- Churn Rate card
- Number of Customers card
- Number of Churned Customers card
- Number of Customers by Churn Reason
- Number of Customers by Contract Type
- Churn Rate by State map

---

# Key Insights

## Highest Churn Rate by State

**Question:** Which state has the highest churn rate for customers with month-to-month contracts?

**Finding:** California had a churn rate of **79%** for this customer group.

---

# Age Groups

The dashboard includes:

- Number of Customers by Age Bin
- Monthly Charge by Customer Group
- Account Length slicer

Page-level filters were applied to investigate customers aged 50 and above with an account length of 12 months or less.

This customer segment had a churn rate of **50.67%**.

---

# Customer Service Calls

A new measure was created to calculate the average number of customer service calls per customer.

### Average Customer Service Calls

Avg Customer Service Calls = SUM('Databel - Data'[Customer Service Calls]) / [Number of Customers]


A new page was created containing:

- Total Customer Service Calls
- Average Customer Service Calls
- Churn Rate
- Average Account Length
- Payment Method
- Contract Category

A scatter plot was created with:

- **X-axis:** Average Account Length
- **Y-axis:** Churn Rate
- **Values:** Payment Method
- **Legend:** Contract Category

The analysis indicated that customers who contact customer service more frequently also tend to have higher-than-average churn.

---

# Extra Charges

A new page called **Extra Charges** was created.

Two new measures were created to calculate average additional charges.

### Average Extra Data Charges

Avg Extra Data Charges = SUM('Databel - Data'[Extra Data Charges]) / [Number of Customers]


### Average Extra International Charges

Avg Extra International Charges = SUM('Databel - Data'[Extra International Charges]) / [Number of Customers]


Both measures were added to cards on the page.

---

# Insights Dashboard

Another page called **Insights** was created.

The following visuals were added:

- Extra Charges cards
- Payment method analysis
- Contract analysis
- Churn Rate by State map

A line chart was also created showing:

- **X-axis:** State
- **Y-axis:** Average Customer Service Calls
- **Legend:** Churn Label
- **Markers:** Enabled

This page brings together the key findings from the previous analysis.

---

# Final Dashboard 

This final dashboard brings together the most prevalent details around the churn at Databel.
- Churn rate
- Number of customers
- Churn rate by reason category
- Churn rate by account type and length
- Churn rate by state

  <img width="1324" height="744" alt="image" src="https://github.com/user-attachments/assets/35611f1d-c743-490b-b6ec-2bec8a53911c" />

---

# Results
## 1. Overall Customer Churn

- The overall churn rate is 26.86%, meaning approximately one in four customers has left Databel.
- The dataset contains 6,687 customers, providing an overview of customer retention and churn patterns.

## 2. Churn Details

- Contract type: Customers on monthly contracts have a significantly higher churn rate than customers on yearly contracts, suggesting that longer-term contracts are associated with better customer retention.
- Age groups: Customers aged 60–80 have the highest churn rates despite representing a smaller customer base than younger age groups.
- Churn reasons: The top three churn categories are Competitor, Attitude, and Dissatisfaction, highlighting potential areas for improving customer retention and satisfaction.
- Geographical differences: California has the fewest customers, with 63 customers, but the highest churn rate at 63.24%, making it a potential priority for further investigation.

## 3. Business Recommendations
Based on the findings, the following actions could help Databel reduce customer churn and improve customer retention.

- Review competitor positioning: Since Competitor is the leading churn category, Databel should investigate competitor pricing, offers, and services to identify opportunities to strengthen its value proposition.
- Improve customer satisfaction: Attitude and Dissatisfaction are among the leading churn reasons. Reviewing customer feedback and support interactions could help identify service issues and improve the overall customer experience.
- Encourage long-term contracts: Customers on monthly contracts have a higher churn rate than those on yearly contracts. Offering incentives, discounts, or additional benefits for yearly subscriptions could encourage customers to commit for longer.
- Target high-risk age groups: Customers aged 60–80 have the highest churn rates. Databel should investigate the reasons behind this pattern and consider targeted retention campaigns tailored to the needs of these customers.
- Investigate churn in California: Despite having only 63 customers, California has a churn rate of 63.24%. Further analysis is needed to determine whether this is driven by pricing, competition, customer experience, or other regional factors before implementing targeted measures.

## Conclusion
The analysis highlights several opportunities for Databel to improve customer retention, particularly by addressing competitive pressure, improving customer satisfaction, and encouraging longer-term contracts. By investigating high-churn customer segments and prioritising retention efforts based on the findings, Databel can make more informed, data-driven decisions to help reduce churn and strengthen customer loyalty.

---

# Tools Used

- **Microsoft Power BI**
- **DAX**
- **Power Query**
- **GitHub**

# Summary

The analysis investigates customer churn across several dimensions, including:

- Demographics
- Age
- Contract type
- Monthly charges
- Data consumption
- International plans
- Payment methods
- Customer service calls
- Customer tenure
- Geographic location

The analysis identifies customer groups with particularly high churn rates and highlights potential opportunities for improving customer retention.
