# E-Commerce Churn Analysis: Unlocking "Revenue at Risk" & Customer Retention

## 📌 Project Overview
In the e-commerce industry, customer acquisition is highly competitive and expensive. Retaining existing customers is the most sustainable path to profitability. This project presents a deep-dive diagnostic analysis into customer churn, moving beyond simple counts to uncover the **real financial impact** of customer attrition. 

By analyzing historical purchase behavior, engagement metrics, and loyalty tiers, this project establishes a proactive **"Revenue at Risk" framework** to identify high-value customers showing early signs of withdrawal before they permanently churn.

---

## 💼 Business Problem & Objective
The primary goal of this analysis is to diagnose the company's churn profile and answer critical executive questions:
1. **How much revenue has been permanently lost to churn?**
2. **Are we losing our most valuable customers (VIP Churn), or is it mostly low-tier experimentation?**
3. **What is our current "Revenue at Risk" from active customers who are drifting away?**

### The Churn Definition
Following the business rules defined in the data dictionary, a customer is flagged as **Churned (1)** if they meet either of the following criteria:
* Inactivity $> 365$ days.
* Inactivity $> 180$ days **AND** a satisfaction score $\le 2$.

---

## 📊 Key Analytical Findings

The diagnostic analysis revealed a critical scenario, often referred to in business as the **"Leaking Bucket" phenomenon**:

### 1. The Financial Bleed (The "Leaking Bucket" & Asymmetric Loss)
* **Massive Revenue Loss:** A staggering **55.12% of the company's historical total revenue** has been permanently lost to churned customers. 
* **The Volume vs. Value Breakdown:** Interestingly, **67.33% of all lost customers account for this 55.12% revenue drop**. This indicates that while the absolute volume of churn is heavily driven by entry-level tiers (e.g., Bronze buyers who shop once and leave), the financial impact is heavily distributed across the board, pulling down over half of the company's historical lifetime value.
* **Critical Retention Rate:** Only **32%** of the entire historical customer base is currently active.
* **The Looming Threat:** Of those remaining active customers, **60% are already sitting in the "Medium Risk" zone** (over 120 days since their last purchase). This means only about 12.8% of the total customer base is currently active and healthy.

### 2. The Behavior Paradox: Price is Not the Issue
* **Uniform Purchasing Power:** Interestingly, the Average Order Value (AOV) between active and churned customers is nearly identical, with a negligible **$5 difference**. 
* **The Insight:** Scatter plots mapping total orders against average order value show perfectly overlapping distributions between active and inactive users. This proves that customers do not gradually buy cheaper items or downsize their carts before leaving—they purchase normally and then abruptly abandon the brand. This strongly points to friction in the post-purchase journey, poor customer service, or aggressive competitor poaching rather than pricing dissatisfaction.

### 3. VIP Churn (The Loyalty Tier Trap)
* **Bronze Tier Churn:** **88%**. While high, a heavy churn rate among entry-level buyers who shop once with a discount code and leave is common in e-commerce.
* **Platinum Tier Churn:** **57%**. This is the highest red flag. Platinum customers are leaving at an alarming rate, historically representing $2.6 million in revenue. Losing more than half of your highest-value segment means the current loyalty program and VIP relationship management are failing to retain the core revenue drivers.

---

## 🛡️ Proactive Risk Framework: "Revenue at Risk"

To shift from a reactive overview to a proactive retention strategy, a dynamic risk segmentation feature (`risk_level_churn`) was engineered using `numpy.select` based on the following logic:

* 🛑 **High Risk:** Active customers (`churn == 0`) with 90 to 180 days of inactivity **AND** a post-purchase satisfaction score $\le 2$.
* ⚠️ **Medium Risk:** Active customers (`churn == 0`) with more than 120 days of inactivity, regardless of satisfaction.
* 🟢 **No Risk:** Active, frequently engaging, and satisfied customers.
* 🪦 **Churned:** Customers who already meet the official churn definition (`churn == 1`).

