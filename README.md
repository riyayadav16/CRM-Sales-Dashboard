# MavenTech CRM Sales Dashboard | Power BI

## About the Project

This is my Power BI project based on the MavenTech CRM Sales dataset from Maven Analytics.

MavenTech is a B2B computer hardware company. The dataset contains information about its sales opportunities, products, customers and sales agents.

I wanted to understand how the company's sales were performing, which products were generating more revenue and how different sales agents and regions were performing.

I used Power BI to explore the data, create different measures and build an interactive dashboard.

## Tools Used

- Power BI
- Power Query
- DAX

## Dataset

The dataset contains four main tables:

| Table          | Information                                                               |
| -------------- | ------------------------------------------------------------------------- |
| Sales Pipeline | Sales opportunities, agents, products, deal stages, dates and deal values |
| Accounts       | Customer details such as sector, revenue, employees and location          |
| Products       | Product names, product series and sales prices                            |
| Sales Teams    | Sales agents, their managers and regional offices                         |

I also used the data dictionary to understand what each column represents.

## Data Modelling

I connected the four tables in Power BI using relationships.

- Products was connected to Sales Pipeline using Product.
- Accounts was connected to Sales Pipeline using Account.
- Sales Teams was connected to Sales Pipeline using Sales Agent.

All three relationships are one-to-many.

Sales Pipeline is the main table because it contains the details of individual sales opportunities. The other tables provide extra information about products, customers and agents.

## Questions I Wanted to Answer

Before creating the dashboard, I thought about some questions that a sales manager might want to understand.

### Overall Sales

1. How much revenue did the company generate from won deals?
2. How many deals were won, lost and are still open?
3. What is the overall win rate?
4. What is the average value of a won deal?
5. How does revenue change from one quarter to another?
6. How many days does it take to close a deal after engagement?

### Sales Agent Performance

1. Which sales agents generate the highest revenue?
2. Which agents have the highest and lowest win rates?
3. Who has closed the most deals?
4. How do agents compare when looking at revenue, deals won and win rate together?

### Product Performance

1. Which products generate the most revenue?
2. Which products have the highest win rates?
3. Is the product generating the most revenue also the one with the highest win rate?

### Regional Performance

1. Which region generates the highest revenue?
2. Which region has the highest win rate?
3. How does sales performance differ across regions?

## KPIs Created Using DAX

I created the following measures to understand the sales performance.

| KPI                   | Meaning                                             |
| --------------------- | --------------------------------------------------- |
| Total Revenue         | Revenue from successfully won deals                 |
| Deals Won             | Number of won opportunities                         |
| Deals Lost            | Number of lost opportunities                        |
| Open Deals            | Number of opportunities still in the Engaging stage |
| Win Rate              | Percentage of closed deals that were won            |
| Win/Loss Ratio        | Comparison of won deals with lost deals             |
| Average Deal Value    | Average revenue from each won deal                  |
| Average Days to Close | Average days between engagement and closing         |

### Some DAX Measures

**1. Total Revenue**

```dax
Total Revenue =
CALCULATE(
    SUM('sales_pipeline'[close_value]),
    'sales_pipeline'[deal_stage] = "Won"
)
```

I used this measure to calculate revenue only from deals that were won.

**2. Deals Won**

```dax
Deals Won =
CALCULATE(
    COUNTROWS('sales_pipeline'),
    'sales_pipeline'[deal_stage] = "Won"
)
```

This counts how many opportunities were successfully won.

**3. Deals Lost**

```dax
Deals Lost =
CALCULATE(
    COUNTROWS('sales_pipeline'),
    'sales_pipeline'[deal_stage] = "Lost"
)
```

This counts how many opportunities were lost.

**4. Open Deals**

```dax
Open Deals =
CALCULATE(
    COUNTROWS('sales_pipeline'),
    'sales_pipeline'[deal_stage] = "Engaging"
)
```

This counts the deals that are still in progress.

**5. Win Rate**

```dax
Win Rate =
DIVIDE(
    [Deals Won],
    [Deals Won] + [Deals Lost],
    0
)
```

This calculates the percentage of closed deals that were won. I did not include Engaging deals because they are still open.

**6. Average Deal Value**

```dax
Average Deal Value =
DIVIDE(
    [Total Revenue],
    [Deals Won],
    0
)
```

This tells us how much revenue the company earns on average from each won deal.

## Dashboard

I created the dashboard to show the important sales information in one place.

It includes:

- KPI cards for Total Revenue, Win/Loss Ratio, Average Days to Close, Win Rate and Average Deal Value.
- Revenue generated by each sales agent.
- Deals won by each sales agent.
- Win rate comparison of top sales agents.
- Quarterly revenue trend.
- Product-wise win rate.
- Revenue contribution by product.
- Revenue contribution by sales region.
- Filters for month, sales region and sales agent.

The filters help users explore the data based on different months, regions and sales agents.

## Key Findings

After exploring the dashboard, I observed the following:

- The total revenue displayed is approximately 207.18K.
- There are 129 won deals, 66 lost deals and 34 open deals.
- The overall win rate is 66.2%.
- The Win/Loss Ratio is approximately 2.
- The average time from engagement to closing is 57 days.
- The average deal value is approximately 1.61K.
- MG Advanced has the highest revenue contribution in the product table.
- GTX Plus has the second-highest revenue contribution.
- GTX Basic has the highest win rate among the products shown.
- Q2 has the highest revenue in the quarterly trend shown.

One thing I noticed is that the product with the highest revenue is not always the product with the highest win rate. Both metrics are important when comparing product performance.

## Conclusion

This project helped me understand how sales data can be used to answer business questions.

I got the opportunity to work with multiple tables, create DAX measures and build an interactive dashboard.

It also helped me understand that looking at revenue alone is not enough to judge sales performance. We also need to look at the number of deals won, win rate, products and regional performance.

This was a good learning experience for me and helped me improve my understanding of Power BI and data analysis.


