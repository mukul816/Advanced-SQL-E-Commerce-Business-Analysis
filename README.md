# Advanced-SQL-E-Commerce-Business-Analysis
Advanced SQL e-commerce analysis using the Olist dataset. Analyzed 99,441 orders, 96,096 customers, 3,095 sellers, and 15.4M+ revenue using SQLite, CTEs, joins, views, window functions, RFM segmentation, delivery analysis, review impact, and business recommendations.
# Advanced SQL E-Commerce Business Analysis Using Olist Dataset

## Project Overview

This project is an end-to-end **E-Commerce Business Analysis** using the **Olist Brazilian E-Commerce Dataset**. The main objective of this project is to analyze marketplace performance using SQL and generate business insights related to revenue, product categories, sellers, customers, delivery performance, review scores, customer retention, and payment behavior.

The project follows an **ETL-based workflow**, where raw CSV files are extracted from the dataset, transformed into structured tables, loaded into a SQLite database, and analyzed using advanced SQL queries.

This project is created from a **Business Analyst / Data Analyst perspective**, focusing not only on writing SQL queries but also on converting raw data into meaningful business insights and practical business recommendations.

---

## Business Objective

The main objective of this project is to answer important business questions such as:

* How is the marketplace performing in terms of orders, revenue, customers, and sellers?
* Which product categories generate the highest revenue?
* Which sellers contribute the most to marketplace revenue?
* Which customer regions generate the highest business value?
* Are customers returning for repeat purchases?
* Which customers are high-value, loyal, normal, or at risk?
* What percentage of orders are delivered late?
* Does late delivery affect customer review scores?
* Which payment methods are most preferred by customers?
* What business recommendations can improve revenue, retention, delivery performance, and customer satisfaction?

---

## Dataset Source

The dataset used in this project is the **Brazilian E-Commerce Public Dataset by Olist**, available on Kaggle.

**Dataset Link:**
https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce/data

This dataset contains real e-commerce marketplace data from Brazil, including customer orders, order items, products, sellers, payments, delivery details, customer reviews, and product category translations.

### Dataset Files Used

* `olist_orders_dataset.csv`
* `olist_order_items_dataset.csv`
* `olist_customers_dataset.csv`
* `olist_products_dataset.csv`
* `olist_sellers_dataset.csv`
* `olist_order_payments_dataset.csv`
* `olist_order_reviews_dataset.csv`
* `product_category_name_translation.csv`

The raw dataset was downloaded from Kaggle, loaded into Pandas DataFrames, converted into SQLite database tables, and analyzed using advanced SQL queries.

---

## Tools & Technologies Used

* Kaggle Notebook
* Python
* Pandas
* SQLite
* SQL
* Matplotlib
* ETL Workflow
* Advanced SQL Querying

---

## ETL Workflow

This project follows a simple ETL process.

### 1. Extract

Raw CSV files were extracted from the Olist dataset and loaded into Pandas DataFrames.

### 2. Transform

The data was prepared for analysis by:

* Checking row counts
* Checking table structure
* Understanding table relationships
* Checking missing values
* Checking duplicate records
* Creating derived fields such as revenue, delivery days, delay days, and customer segments
* Creating SQL views for easier analysis

### 3. Load

The transformed DataFrames were loaded into a SQLite database. SQL queries were then executed inside the Kaggle Notebook to perform business analysis.

---

## Database Tables Used

| Table Name             | Description                                                                      |
| ---------------------- | -------------------------------------------------------------------------------- |
| `orders`               | Contains order status, purchase date, delivery date, and estimated delivery date |
| `order_items`          | Contains product price, freight value, seller ID, and product ID                 |
| `customers`            | Contains customer location and unique customer ID                                |
| `products`             | Contains product category and product-level details                              |
| `sellers`              | Contains seller location and seller ID                                           |
| `payments`             | Contains payment type, payment value, and installments                           |
| `reviews`              | Contains customer review score and review details                                |
| `category_translation` | Contains English translation of product category names                           |

---

## Key Table Relationships

| Relationship                        | Joining Key             |
| ----------------------------------- | ----------------------- |
| `orders` → `order_items`            | `order_id`              |
| `orders` → `customers`              | `customer_id`           |
| `orders` → `payments`               | `order_id`              |
| `orders` → `reviews`                | `order_id`              |
| `order_items` → `products`          | `product_id`            |
| `order_items` → `sellers`           | `seller_id`             |
| `products` → `category_translation` | `product_category_name` |

---

## Advanced SQL Concepts Used

This project uses both basic and advanced SQL techniques, including:

* Joins
* Aggregations
* Common Table Expressions, also known as CTEs
* SQL Views
* Window Functions
* `RANK()`
* `LAG()`
* `NTILE()`
* `CASE WHEN`
* Conditional Aggregation
* Date Functions using `strftime()` and `julianday()`
* Revenue Contribution Analysis
* Month-over-Month Growth Analysis
* RFM Customer Segmentation
* Delivery Delay Classification
* Review Score Impact Analysis

---

# Business KPI Overview

The first step of the analysis was to calculate high-level marketplace KPIs.

| Metric                              |         Value |
| ----------------------------------- | ------------: |
| Total Orders                        |        99,441 |
| Delivered Orders                    |        96,478 |
| Unique Customers                    |        96,096 |
| Total Sellers                       |         3,095 |
| Total Product Categories            |            73 |
| Total Revenue from Delivered Orders | 15,419,773.75 |
| Average Order Value                 |        159.83 |
| Average Review Score                |      4.09 / 5 |

## KPI Insights

The Olist marketplace shows strong overall business activity with **99,441 total orders**, out of which **96,478 orders were successfully delivered**. This indicates that most customer orders were fulfilled successfully.

The platform served **96,096 unique customers** and had **3,095 active sellers**, showing that Olist operated as a large multi-seller e-commerce marketplace.

The marketplace generated **15,419,773.75** in revenue from delivered orders, with an **average order value of 159.83**. The average customer review score was **4.09 out of 5**, indicating generally positive customer satisfaction.

---

# Sales, Product & Seller Performance Analysis

## Monthly Sales Performance

| Metric                          | Finding      |
| ------------------------------- | ------------ |
| Highest Revenue Month           | 2017-11      |
| Revenue in Highest Month        | 1,153,364.20 |
| Lowest Revenue Month            | 2016-12      |
| Revenue in Lowest Month         | 19.62        |
| Total Delivered Orders Analyzed | 96,478       |
| Average Monthly Order Value     | 154.39       |

## Insight

The highest revenue month was **November 2017**, generating **1,153,364.20** in revenue. This indicates a strong sales peak, possibly due to seasonal campaigns, promotional activity, or year-end shopping behavior.

The lowest revenue month was **December 2016**, with only **19.62** in revenue. This appears to be an early-stage or low-activity period in the dataset.

### Suggested Image

Upload this image to:

```text
images/monthly_revenue_trend.png
```

Use this in README:

```markdown
![https://github.com/mukul816/Advanced-SQL-E-Commerce-Business-Analysis/blob/main/Advanced%20SQL%20E-Commerece%20Olist%20Business%20Analysis/Images/Monthly%20Revenue%20Trend.png]
```

---

## Month-over-Month Revenue Growth

| Metric             | Finding     |
| ------------------ | ----------- |
| Best Growth Month  | 2017-01     |
| Best Growth Rate   | 649,657.24% |
| Worst Growth Month | 2016-12     |
| Worst Growth Rate  | -99.96%     |

## Insight

The strongest month-over-month growth occurred in **January 2017**, with a very high growth rate of **649,657.24%**. This extreme growth occurred because the previous month had a very small revenue base.

The worst month-over-month performance occurred in **December 2016**, with a decline of **-99.96%**.

This analysis helps identify strong growth periods, weak months, and possible seasonality in marketplace performance.

---

## Product Category Performance

| Metric               | Finding       |
| -------------------- | ------------- |
| Top Revenue Category | health_beauty |
| Revenue Generated    | 1,412,089.53  |
| Total Orders         | 8,647         |

## Insight

The **health_beauty** category was the highest revenue-generating category, producing **1,412,089.53** in revenue from **8,647 orders**.

This category is a major revenue driver and should be prioritized for marketing campaigns, inventory planning, and seller partnerships.

### Suggested Image

Upload this image to:

```text
images/top_categories_by_revenue.png
```

Use this in README:

```markdown
![Top Product Categories by Revenue](images/top_categories_by_revenue.png)
```

---

## Product Category Revenue Contribution

| Metric                        | Finding                                      |
| ----------------------------- | -------------------------------------------- |
| Top 3 Categories              | health_beauty, watches_gifts, bed_bath_table |
| Combined Revenue Contribution | 25.64%                                       |

## Insight

The top three categories — **health_beauty, watches_gifts, and bed_bath_table** — contributed **25.64%** of total marketplace revenue.

This shows that revenue is meaningfully concentrated in a few high-performing categories. These categories should be protected and expanded through promotions, better inventory availability, and stronger seller partnerships.

---

## Seller Performance

| Metric            | Finding                          |
| ----------------- | -------------------------------- |
| Top Seller ID     | 4869f7a5dfa277a7dca6462dcf3b52b2 |
| Seller Location   | guariba, SP                      |
| Revenue Generated | 247,007.06                       |
| Total Orders      | 1,124                            |

## Insight

The top seller generated **247,007.06** in revenue from **1,124 orders**. This seller is one of the strongest contributors to marketplace revenue.

High-performing sellers like this should be supported through better visibility, performance monitoring, seller dashboards, and promotional support.

---

## Seller Revenue Contribution

| Metric                             | Finding |
| ---------------------------------- | ------- |
| Top 5 Sellers Revenue Contribution | 7.44%   |

## Insight

The top 5 sellers together contributed **7.44%** of total marketplace revenue.

This indicates that although the marketplace has thousands of sellers, a small group of sellers contributes significantly to revenue. The business should maintain strong relationships with top sellers while helping mid-level sellers grow.

---

## Seller State Performance

| Metric                        | Finding      |
| ----------------------------- | ------------ |
| Top Seller State              | SP           |
| Total Sellers in SP           | 1,769        |
| Total Revenue from SP Sellers | 9,957,056.91 |
| Revenue per Seller            | 5,628.64     |

## Insight

The seller state **SP** generated the highest revenue, with **9,957,056.91** from **1,769 sellers**.

This shows that São Paulo is the strongest seller hub for the marketplace. Olist should continue strengthening this region while developing seller performance in other states.

### Suggested Image

Upload this image to:

```text
images/seller_state_performance.png
```

Use this in README:

```markdown
![Seller State Performance](images/seller_state_performance.png)
```

---

## Low-Performing Product Category

| Metric                     | Finding           |
| -------------------------- | ----------------- |
| Lowest-Performing Category | cds_dvds_musicals |
| Revenue Generated          | 954.99            |
| Total Orders               | 12                |

## Insight

The **cds_dvds_musicals** category generated only **954.99** in revenue from **12 orders**. This category may require better promotion, pricing review, product assortment improvement, or strategic reconsideration.

---

# Customer, Delivery & Satisfaction Analysis

## Customer Geography Analysis

| Metric             | Finding      |
| ------------------ | ------------ |
| Top Customer State | SP           |
| Total Customers    | 39,149       |
| Total Orders       | 40,494       |
| Total Revenue      | 5,798,099.03 |

## Insight

The customer state **SP** generated the highest revenue with **5,798,099.03**, coming from **39,149 customers** and **40,494 orders**.

This confirms that São Paulo is the strongest customer market as well as the strongest seller hub.

---

## Repeat Customer Analysis

| Customer Type     | Total Customers | Average Orders per Customer | Total Revenue | Average Customer Value |
| ----------------- | --------------: | --------------------------: | ------------: | ---------------------: |
| One-Time Customer |          90,549 |                        1.00 | 14,564,258.64 |                 160.84 |
| Repeat Customer   |           2,801 |                        2.11 |    924,027.99 |                 329.89 |

## Insight

The marketplace had **90,549 one-time customers** and only **2,801 repeat customers**. The repeat customer rate was approximately **3.00%**.

Although repeat customers were much fewer, their average customer value was **329.89**, which is significantly higher than the **160.84** average value of one-time customers.

This shows a major opportunity to improve customer retention.

---

## RFM Customer Segmentation

| Customer Segment               | Total Customers | Average Frequency | Average Monetary Value |
| ------------------------------ | --------------: | ----------------: | ---------------------: |
| Normal Customers               |          45,674 |              1.03 |                 166.33 |
| At-Risk Customers              |          23,688 |              1.00 |                  63.89 |
| Loyal Customers                |          11,932 |              1.08 |                 260.62 |
| Best Customers                 |          11,892 |              1.07 |                 273.33 |
| Potential High Value Customers |             164 |              1.00 |                 108.25 |

## Insight

The largest segment was **Normal Customers**, with **45,674 customers**.

The analysis also identified **23,688 At-Risk Customers**, which is a major concern for retention. Best Customers and Loyal Customers had higher average monetary values of **273.33** and **260.62**, respectively.

RFM segmentation can help the business design targeted marketing campaigns for different customer groups.


## Delivery Performance

| Metric                      | Finding |
| --------------------------- | ------: |
| Late Delivered Orders       |   7,826 |
| Late Delivery Percentage    |   8.11% |
| On-Time Delivery Percentage |  91.89% |

## Insight

Most orders were delivered on time, but **7,826 orders** were delivered late, representing **8.11%** of delivered orders.

Late delivery is a critical operational issue because it directly affects customer satisfaction and review scores.

---

## State Delivery Delay Analysis

| Metric                                      | Finding |
| ------------------------------------------- | ------- |
| State with Highest Late Delivery Percentage | AL      |
| Total Orders in AL                          | 397     |
| Late Delivery Percentage                    | 26.20%  |
| Average Delivery Days                       | 24.48   |

## Insight

The state **AL** had the highest late delivery percentage at **26.20%**, with an average delivery time of **24.48 days**.

This region needs logistics improvement, better delivery planning, and stronger courier performance monitoring.

---

## Review Score Distribution

| Metric                    | Finding |
| ------------------------- | ------- |
| Most Common Review Score  | 5       |
| Orders with 5-Star Review | 56,810  |
| 5-Star Review Share       | 59.29%  |

## Insight

The most common review score was **5**, with **56,810 orders** receiving a 5-star rating. This represented **59.29%** of all reviewed orders.

This shows that most customers had a positive experience, but delayed orders received much lower review scores.

---

## Delivery Impact on Review Score

| Delivery Status | Total Orders | Average Review Score | Positive Review % | Negative Review % |
| --------------- | -----------: | -------------------: | ----------------: | ----------------: |
| On Time         |       88,163 |                 4.21 |            80.40% |            11.43% |
| Late            |        7,661 |                 2.55 |            34.25% |            54.64% |

## Insight

On-time deliveries had an average review score of **4.21**, while late deliveries had an average review score of only **2.55**.

The review score difference was **1.66 points**, showing that delivery delays strongly reduce customer satisfaction.

Late deliveries also had a **54.64% negative review rate**, compared to only **11.43%** for on-time deliveries.


## Delay Category vs Review Score

| Delay Category        | Average Review Score |
| --------------------- | -------------------: |
| On Time or Early      |                 4.21 |
| 1–3 Days Late         |                 3.47 |
| 4–7 Days Late         |                 2.17 |
| More Than 7 Days Late |                 2.39 |

## Insight

The best review group was **On Time or Early**, with an average score of **4.21**.

The worst review group was **4–7 Days Late**, with an average review score of **2.17**.

This confirms that delivery delay severity has a strong negative effect on customer satisfaction.

---

## Payment Behavior Analysis

| Payment Type | Total Payment Records | Total Orders | Total Payment Value | Average Payment Value | Average Installments |
| ------------ | --------------------: | -----------: | ------------------: | --------------------: | -------------------: |
| credit_card  |                76,795 |       76,505 |       12,542,084.19 |                163.32 |                 3.51 |
| boleto       |                19,784 |       19,784 |        2,869,361.27 |                145.03 |                 1.00 |
| voucher      |                 5,775 |        3,866 |          379,436.87 |                 65.70 |                 1.00 |
| debit_card   |                 1,529 |        1,528 |          217,989.79 |                142.57 |                 1.00 |
| not_defined  |                     3 |            3 |                0.00 |                  0.00 |                 1.00 |

## Insight

The most valuable payment method was **credit_card**, contributing **12,542,084.19** in total payment value across **76,505 orders**.

Credit cards dominate both transaction value and order volume, showing strong customer preference for card-based payments.

---

# Key Business Recommendations

## 1. Improve logistics in high-delay states

States such as **AL** showed high late delivery rates. AL had a late delivery percentage of **26.20%**, much higher than the overall late delivery rate of **8.11%**.

Recommended actions:

* Improve logistics partnerships
* Monitor region-wise delivery delays
* Improve estimated delivery accuracy
* Track seller dispatch delays
* Strengthen courier performance in high-delay states

---

## 2. Focus marketing on high-performing categories

The top category **health_beauty** generated **1,412,089.53** in revenue. The top three categories contributed **25.64%** of marketplace revenue.

Recommended actions:

* Run promotional campaigns for top categories
* Improve inventory availability
* Support sellers in high-performing categories
* Use seasonal offers for strong-demand categories

---

## 3. Improve customer retention

Only **2,801 customers** were repeat customers, compared to **90,549 one-time customers**. The repeat customer rate was only **3.00%**.

However, repeat customers had a much higher average customer value of **329.89**, compared to **160.84** for one-time customers.

Recommended actions:

* Launch loyalty programs
* Offer repeat purchase discounts
* Send personalized recommendations
* Use reactivation campaigns
* Target customers based on purchase history

---

## 4. Use RFM segmentation for targeted marketing

The RFM analysis identified:

* **11,892 Best Customers**
* **11,932 Loyal Customers**
* **23,688 At-Risk Customers**
* **45,674 Normal Customers**

Recommended actions:

* Reward Best Customers with loyalty benefits
* Send exclusive offers to Loyal Customers
* Reactivate At-Risk Customers with discounts
* Move Normal Customers toward repeat purchase behavior

---

## 5. Support high-performing sellers

The top seller generated **247,007.06** in revenue, and the top 5 sellers contributed **7.44%** of marketplace revenue.

Recommended actions:

* Maintain strong relationships with top sellers
* Give top sellers better visibility
* Help mid-level sellers improve performance
* Monitor seller delivery and review performance
* Create seller performance dashboards

---

## 6. Reduce delivery delays to improve customer satisfaction

Late deliveries had an average review score of only **2.55**, compared to **4.21** for on-time deliveries.

Recommended actions:

* Reduce delivery delays
* Improve estimated delivery dates
* Track delay reasons
* Improve communication with customers
* Focus on states with high late delivery percentage

---

## 7. Strengthen São Paulo as a core business hub

São Paulo was the strongest seller and customer region.

* Seller state SP generated **9,957,056.91** in revenue
* Customer state SP generated **5,798,099.03** in revenue
* SP had **1,769 sellers**
* SP had **39,149 customers**

Recommended actions:

* Continue strengthening SP as a key business region
* Use SP as a model for marketplace expansion
* Apply successful seller and logistics practices from SP to other states

---

# Final Conclusion

This project analyzed the Olist e-commerce marketplace using an ETL-based SQL workflow. The analysis covered business KPIs, sales trends, product performance, seller contribution, customer behavior, RFM segmentation, delivery performance, review scores, and payment behavior.

The marketplace shows strong overall performance, with **99,441 total orders**, **96,478 delivered orders**, **96,096 unique customers**, **3,095 sellers**, and **15,419,773.75** in delivered-order revenue.

The analysis found that revenue is strongly driven by selected categories such as **health_beauty**, **watches_gifts**, and **bed_bath_table**. São Paulo is the strongest business region for both sellers and customers.

However, the business has clear improvement opportunities in customer retention and logistics performance. The repeat customer rate is only **3.00%**, and late deliveries reduce average review scores from **4.21** to **2.55**.

Overall, this project demonstrates how advanced SQL can be used to convert raw e-commerce data into business insights and actionable recommendations.

---


# Skills Demonstrated

* SQL Querying
* Advanced SQL Analysis
* ETL Workflow
* SQLite Database Creation
* Data Cleaning and Validation
* Business KPI Analysis
* Revenue Analysis
* Product Performance Analysis
* Seller Performance Analysis
* Customer Segmentation
* RFM Analysis
* Delivery Performance Analysis
* Review Score Impact Analysis
* Payment Behavior Analysis
* Business Insight Generation
* Data-Driven Recommendations

---


