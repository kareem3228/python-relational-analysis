# Olist E-Commerce: Replicating SQL Logic in Python

## Why this exists
I’ve been writing a lot of SQL queries lately, so I wanted to see if I could replicate that same relational logic purely in Python (Pandas).

Instead of treating the data as flat CSVs, I treated them like relational tables. I used `.merge()` to simulate **INNER**, **LEFT**, **RIGHT**, and **OUTER** joins to answer actual business questions about the Olist dataset.

## The Data
I used the Olist E-Commerce dataset (5 CSVs):
* `Customers` & `Orders` (Who bought what)
* `Order_Items` & `Products` (What they actually bought)
* `Payments` (How they paid)

## What I did

### 1. Replicating Joins (The Technical Part)
I didn't just merge everything into one giant mess. I used specific join types for specific questions:
* **Inner Merges:** To link Customers to Orders (we only care about customers who actually bought something).
* **Left Merges:** To bring in Payment data without losing the original Order context.
* **Aggregations:** Replicated `GROUP BY` logic to find top sellers and revenue per category.

### 2. The Findings
* **The "SP" Domination:** São Paulo (SP) has more orders than almost every other region combined.
* **The "Ghost" Orders:** By performing a data integrity check (using a Left Join between `Orders` and `Items`), I found **775 orders** that exist in the system but have 0 items attached to them. This is likely a system error or cancelled transactions that weren't cleaned up.
* **Top Category:** "Health & Beauty" moves the most volume, but PCs have the highest average ticket price.

### 3. Tools
* **Pandas:** For all the relational merging and grouping.
* **Matplotlib:** To visualize the regional dominance and seller stats.

## How to run it
1. Clone this repo.
2. Drop the Olist CSV files into the folder (I didn't upload them because they are huge).
3. Run `olist_analysis.ipynb`.
