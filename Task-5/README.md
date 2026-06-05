# Task 5 - Exploratory Data Analysis (EDA)

## Internship
Data Analyst Internship

---

# Objective

The objective of this task was to perform Exploratory Data Analysis (EDA) on the Titanic Dataset using Python. The analysis focused on understanding data distributions, identifying patterns, detecting anomalies, and extracting meaningful insights through statistical summaries and visualizations.

---

# Dataset Used

**Titanic Dataset (train.csv)**

The dataset contains information about Titanic passengers, including:

- Passenger ID
- Survival Status
- Passenger Class
- Name
- Sex
- Age
- Number of Siblings/Spouses
- Number of Parents/Children
- Ticket
- Fare
- Cabin
- Embarked Port

### Target Variable

**Survived**

- 0 = Did Not Survive
- 1 = Survived

---

# Tools Used

- Python
- Jupyter Notebook
- Pandas
- NumPy
- Matplotlib
- Seaborn
- GitHub

---

# Data Exploration

The dataset was explored using:

```python
df.info()
df.describe()
df.value_counts()
df.isnull().sum()
```

The analysis included:

- Dataset overview
- Data types inspection
- Missing value detection
- Statistical summary

---

# Visualizations Created

## 1. Missing Values Heatmap

Used to identify missing values across columns.

### Observation

- Cabin contains a large number of missing values.
- Age contains moderate missing values.
- Embarked contains very few missing values.

---

## 2. Age Distribution Histogram

Analyzed passenger age distribution.

### Observation

Most passengers were between 20 and 40 years old.

---

## 3. Fare Distribution Histogram

Analyzed ticket fare distribution.

### Observation

Fare distribution is positively skewed.

---

## 4. Age Boxplot

Used to identify age outliers.

### Observation

A few age outliers are present.

---

## 5. Fare Boxplot

Used to detect fare outliers.

### Observation

Several extreme fare values are present.

---

## 6. Survival by Gender

Compared survival rates across genders.

### Observation

Female passengers had significantly higher survival rates than male passengers.

---

## 7. Survival by Passenger Class

Compared survival across passenger classes.

### Observation

First-class passengers had better survival chances.

---

## 8. Age vs Fare Scatter Plot

Analyzed the relationship between age and fare.

### Observation

Passengers paying higher fares showed higher survival probability.

---

## 9. Correlation Heatmap

Analyzed relationships among numerical variables.

### Observation

- Fare positively correlates with survival.
- Passenger class negatively correlates with survival.

---

## 10. Pairplot

Performed multivariate analysis.

### Observation

Relationships among Age, Fare, Pclass, and Survival can be visually observed.

---

# Key Findings

- Female passengers had higher survival rates.
- First-class passengers survived more frequently.
- Fare positively influenced survival probability.
- Most passengers belonged to the 20–40 age group.
- Fare distribution was highly skewed.
- Cabin contained a significant amount of missing data.
- Passenger class strongly affected survival outcomes.

---

# Skills Learned

- Data Cleaning
- Exploratory Data Analysis (EDA)
- Statistical Analysis
- Data Visualization
- Correlation Analysis
- Outlier Detection
- Data Storytelling

---

# Outcome

Successfully performed Exploratory Data Analysis on the Titanic dataset and extracted meaningful insights through statistical summaries and visualizations. Developed practical experience in identifying patterns, trends, relationships, and anomalies in real-world data.

---

# Files Included

- train.csv
- Task5_EDA_Titanic.ipynb
- Task5_EDA_Report.pdf
- Visualization Screenshots
- README.md

---

# Author

**Pavan Kalyan**

Data Analyst Intern