# 📊 EDA – Bank Loan Default Analysis

This repository contains an **Exploratory Data Analysis (EDA)** project on bank loan application data. The goal is to understand **patterns behind loan default (TARGET)** and identify **key risk factors** using data cleaning, visualization, and statistical insights.

---

## 📁 Project Structure

```
EDA-Bank-Loan/
│── EDA Bank loan.ipynb   # Main EDA notebook
│── README.md            # Project documentation
```

---

## 🎯 Objective

- Analyze customer **demographics, employment, income, and credit history**
- Study relationships between **categorical & numerical features** and **loan default (TARGET)**
- Identify **high-risk customer segments**
- Prepare insights useful for **credit risk modeling**

---

## 🛠️ Tech Stack

- **Python 3**
- **Pandas** – data manipulation
- **NumPy** – numerical operations
- **Matplotlib & Seaborn** – visualization
- **Jupyter Notebook** – analysis environment

---

## 📦 Libraries Used (Code)

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

plt.style.use('seaborn-v0_8')
```

---

## 📊 Data Overview

- **TARGET**:
  - `0` → Loan repaid (Non-defaulter)
  - `1` → Loan defaulted (Defaulter)

- Dataset contains:
  - Categorical features (employment, education, housing, etc.)
  - Numerical features (income, credit amount, age, etc.)

---

## 🧹 Data Cleaning & Preprocessing

### Drop Unnecessary Columns & Handle Missing Values

```python
# Drop columns with high missing values
missing_percent = df.isnull().mean() * 100
cols_to_drop = missing_percent[missing_percent > 40].index
df = df.drop(columns=cols_to_drop)

# Fill numerical missing values with median
num_cols = df.select_dtypes(include=np.number).columns
df[num_cols] = df[num_cols].fillna(df[num_cols].median())
```

---

### Clean Categorical Values

```python
cat_cols = df.select_dtypes(include='object').columns

for col in cat_cols:
    df[col] = df[col].str.strip().str.upper()
```

---

## 📈 Exploratory Data Analysis

### 1️⃣ Default Rate by Categorical Features

```python
def plot_default_rate(col):
    rate = df.groupby(col)['TARGET'].mean().sort_values(ascending=False)
    plt.figure(figsize=(8,4))
    rate.plot(kind='bar')
    plt.ylabel('Default Rate')
    plt.title(f'Default Rate by {col}')
    plt.show()

plot_default_rate('NAME_INCOME_TYPE')
```

**Insights Example:**

- Unemployed customers show the **highest default rate**
- Business owners have **lower default risk**

---

### 2️⃣ Numerical Feature Analysis

```python
plt.figure(figsize=(6,4))
sns.histplot(df[df['TARGET']==1]['AMT_INCOME_TOTAL'], kde=True, label='Defaulters')
sns.histplot(df[df['TARGET']==0]['AMT_INCOME_TOTAL'], kde=True, label='Non-Defaulters')
plt.legend()
plt.title('Income Distribution vs Default')
plt.show()
```

---

### 3️⃣ Correlation Analysis

```python
plt.figure(figsize=(10,6))
sns.heatmap(df[num_cols].corr(), cmap='coolwarm', annot=False)
plt.title('Correlation Heatmap')
plt.show()
```

---

## 🔍 Key Insights

- 🚨 **Unemployed applicants** have the highest probability of default
- 💰 **Higher income & stable employment** → lower default risk
- 🏠 **Housing ownership** positively impacts repayment behavior
- 📉 Certain credit amount ranges are strongly associated with default

---

## 👤 Author

**Suraj Prasad**
Full Stack Developer | Exploring AI, LLMs & GenAI

---
