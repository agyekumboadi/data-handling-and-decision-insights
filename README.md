# Data Handling & Decision Making (eBay Seller Ratings Case Study)

Two applied analytics case studies focused on **data cleaning, statistical testing, and decision insights**, with a main case study analysing how **eBay seller ratings influence customer purchasing behaviour** using an inferential (regression) approach.

---

## Project Snapshot

**Business question:**  
Do existing seller ratings influence other customers’ decision to purchase products?

**Hypotheses:**  
- **H0:** Existing seller ratings have no impact on customers’ decision to purchase products.  
- **H1:** Existing seller ratings impact customers’ decision to purchase products.

**Outcome (summary):**  
The analysis supports **H1**, showing a **strong exponential relationship** between seller rating and review volume (used as a proxy for purchase activity). The insight supports a **strategic decision** to prioritise rating improvement initiatives to drive customer trust, visibility, and sales performance.

---

## Repository Structure

- **/report** → The full academic case study report (PDF)
- **/docs** → Extracted visuals and supporting images referenced in the report

Recommended structure:
├── README.md
├── docs/
│ ├── README.md
│ └── images/
└── report/
├── README.md
└── Case_Study_Report_Data_Handling_and_Decision_Making.pdf

---

## Dataset Overview

**Source & method of acquisition:**  
Secondary dataset published on Kaggle, created through web scraping by PromptCloud and DataStock.

**Representativeness:**  
- Large dataset representing a wide range of eBay product listings (focused on electronics/accessories).
- Useful for modelling behavioural patterns around trust signals (seller ratings) and downstream engagement (reviews).

**Initial dataset size:**  
- **19,230 rows × 30 columns**

**Key study variables:**  
- **Independent variable (X):** Seller Rating  
- **Dependent variable (Y):** Seller Number of Reviews  
  > In this study, review volume is treated as a proxy for purchase activity, since reviews occur after purchase on structured marketplaces.

---

## Data Preparation & Processing Pipeline

### 1) Memory-efficient loading (large CSV handling)
To prevent high memory usage, the dataset was read in **chunks** (100 rows per chunk) and combined using `concat()` after iteration.

**Why this matters:**  
Chunking supports stable processing on limited RAM machines and provides a scalable method for large datasets.

### 2) Cleaning and filtering
Key preparation actions:
- Removed unused/unrelated columns (retaining only study variables for modelling).
- Removed missing values from Seller Rating and Seller Num of Reviews (dropna).
- Ensured numeric type consistency before modelling.

**Final modelling dataset size:**  
- **11,018 rows × 2 columns**

---

## Descriptive Statistics (Cleaned Dataset)

From the cleaned dataset (N = 11,018):

**Seller Rating**
- Mean: **0.985**
- Median: **0.987**
- Std. Dev: **0.0102**
- Min: **0.943**
- Max: **1.00**

**Seller Num of Reviews**
- Mean: **779**
- Median: **354**
- Std. Dev: **975**
- Min: **0**
- Max: **4,121**

These distributions show that seller ratings are tightly clustered close to 1.0, while review counts are heavily right-skewed (many sellers with low reviews and a minority with very high engagement).

---

## Modelling Approach

### Why regression analysis?
Regression was selected because:
- The study focuses on **one predictor** (seller rating) and **one outcome** (review volume).
- It supports **inference** (testing relationships) and **forecasting** (predicting likely review volume under different rating levels).

### Model form: Exponential Regression
Scatter plots showed a clear **non-linear** trend: review volumes rise sharply as ratings approach 1.0.  
Therefore, the modelling assumption was an exponential form:

\[
y = a \cdot b^x
\]

Where:
- \(x\) = seller rating
- \(y\) = seller number of reviews
- \(a, b\) = model constants

---

## Key Results & Interpretation

### 1) Relationship strength
**R² = 0.9913**  
This indicates the exponential model explains about **99.13%** of the variability in review volume using seller rating alone — an exceptionally strong fit for behavioural marketplace data.

### 2) Practical meaning
- At low rating levels (example: **x = 0.971**), predicted reviews remain very small (example point shown around **y = 16**).
- As seller rating approaches **x = 1.0**, review volume increases rapidly, reaching observed maxima such as **y = 4,121** reviews.

This supports the interpretation that **small improvements near high ratings can yield disproportionately large increases in customer engagement and purchasing trust signals**.

---

## Decision Recommendation (Strategic)

**Decision:** Existing seller ratings influence customer purchasing behaviour.  
**Type:** Strategic decision.

**Recommended actions:**
- Improve customer service responsiveness (fast replies, dispute resolution).
- Focus on product quality consistency (reduce returns and negative feedback).
- Provide seller training and best-practice guidance to sustain high rating performance.
- Monitor rating trends and intervene early for sellers drifting below the high-performing range.

**Note:**  
Seller rating is not the only factor influencing purchases. Future modelling improvements should incorporate other explanatory variables such as price, product category, delivery time, and return rate.

---

## Tools & Technologies Used

- **Python** (data loading, filtering, manipulation, and plotting)
  - Typical stack used in the report: pandas, NumPy, Matplotlib (and related libraries)
- **Jamovi** (descriptive statistics, box plots, outlier inspection)
- **Desmos** (equation modelling, exponential curve inspection, forecasting interpretation)

---

## How to Navigate This Repo

1. Start with **/report** to read the full academic write-up.
2. Use **/docs/images** to view the visuals referenced across the report:
   - missing values
   - outlier plots
   - scatter plots
   - exponential growth and forecast graphs

---

## Author

**Samuel Boadi Agyekum**  
MSc Data Analytics & IT Security Management — Arden University  
GitHub: https://github.com/agyekumboadi
