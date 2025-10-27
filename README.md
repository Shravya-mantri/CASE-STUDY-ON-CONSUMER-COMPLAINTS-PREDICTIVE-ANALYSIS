# CASE-STUDY-ON-CONSUMER-COMPLAINTS-PREDICTIVE-ANALYSIS

# 📊 Predictive Analytics: Consumer Complaint Analysis

The project involves analyzing a real-world dataset of consumer complaints lodged with a regulatory body to extract actionable insights and build predictive models.

## 📝 Business Problem

A national regulatory body receives a high volume of consumer complaints against various companies. Each complaint is recorded, and the company is given an aggregate "fitness score" (`Score_ATC`) reflecting its responsibility in addressing these issues.

The regulator faces challenges in understanding systemic issues, identifying high-risk companies, and correlating complaint patterns with company performance. This project aims to provide analytic solutions to support their decision-making.

## 🎯 Project Objectives

This analysis is divided into three core tasks as specified by the case study brief:

1.  **🔍 Task 1: Exploratory & Cluster Analysis**
    * Analyze and visualize the data to understand its structure.
    * Perform cluster analysis to segment companies based on region, sector, and complaint-related attributes.

2.  **📈 Task 2: Predictive Modelling**
    * Develop a predictive model to estimate a company's "fitness score" (`Score_ATC`) based on relevant data attributes.
    * Evaluate and compare different models to select the most accurate one.

3.  **🔗 Task 3: Association Rule Mining**
    * Identify the top 10 most frequently co-occurring complaints across all companies.
    * This helps the regulator identify systemic, interconnected issues that may require policy-level intervention.

## 🛠️ Methodology & Tools

* **Primary Tool:** **Altair AI Studio (RapidMiner)**
* **Techniques:**
    * **Data Preparation:** Joined `Companies` and `Complaints` datasets, replaced missing values (mean imputation), filtered invalid entries, and normalized data.
    * **Clustering (Task 1):** K-Means Clustering (optimized for $k=3$ using Davies-Bouldin index) and Principal Component Analysis (PCA) for visualization.
    * **Prediction (Task 2):** **Linear Regression** and **Gradient Boosted Trees** (GBT), evaluated using 10-fold Cross-Validation.
    * **Association (Task 3):** **FP-Growth** algorithm and **Create Association Rules** operator (min. support: 0.19, min. lift: 2.0).

## 💡 Key Findings & Results

### 1. Cluster Analysis (K-Means, k=3)

Three distinct company profiles were identified:

* **Cluster 0 (Blue):** *The Inactive Group* (4,279 companies).
    * Characterized by significantly lower-than-average customer transactions and fewer recent complaints.
* **Cluster 1 (Green):** *The High-Volume Hospitality Group* (2,346 companies).
    * Dominated by the Hospitality sector with the highest average customer transactions.
* **Cluster 2 (Red):** *The "At-Risk" Group* (4,714 companies).
    * This group has the most recent complaints and a **fitness score that is 40.6% lower** than average, indicating poor complaint handling.

### 2. Predictive Model (Linear Regression)

The **Linear Regression** model was selected as the final model, as it outperformed Gradient Boosted Trees with a lower RMSE.

* **Root Mean Squared Error (RMSE):** **1.189** (The model's predictions are, on average, off by ~1.19 points on the fitness score scale).
* **Squared Correlation ($R^2$):** **0.662** (The model successfully explains **66.2%** of the variance in company fitness scores).

**Key Drivers of Fitness Score:**
* **Strongest Predictor:** `Avg_Cust_Rating_ATC` (Higher customer rating = higher fitness score).
* **Significant Factors:**
    * **Region:** Companies in `Metro-CBD` have higher scores, while those in `Regional` areas have significantly lower scores.
    * **Sector:** `Finance` and `Technology` sectors are associated with higher fitness scores.
    * **Time:** `Months_Last_Complaint_ATC` (More time since the last complaint) positively impacts the score.

### 3. Association Rule Mining (Top 10)

The analysis uncovered strong, non-random relationships between specific complaint codes.

* **Systemic Issue Identified:** Complaints **`CC-361`**, **`CC-834`**, and **`CC-972`** are a tightly linked systemic issue.
* **Perfect Confidence Rules:** Several rules were found with 100% confidence:
    * `{CC-834, CC-972} \rightarrow {CC-361}` (If 834 and 972 occur, 361 *always* occurs).
    * `{CC-361, CC-972} \rightarrow {CC-834}` (If 361 and 972 occur, 834 *always* occurs).
* **High Lift:** The top rules had very high lift values such as **9.087**, proving these complaints co-occur far more often than by random chance. This provides a clear starting point for the regulator to investigate.


