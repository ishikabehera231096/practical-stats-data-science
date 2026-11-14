# Bike Sharing Demand: Exploratory Data Analysis

## 1. Project Overview

This project explores hourly bike-sharing rental data from the [UCI Bike Sharing Dataset](https://archive.ics.uci.edu/dataset/275/bike+sharing+dataset) as part of my study of *Practical Statistics for Data Scientists*.

The objective is to understand how bike rental demand changes throughout the day and how factors such as customer type, weather, temperature, season, and working days relate to rental patterns.

The analysis focuses on a business scenario in which a bike-sharing company wants to better understand customer behaviour and identify opportunities to improve fleet planning, customer retention, and demand forecasting.

**Key questions explored:**
- How does bike rental demand vary throughout the day?
- How do casual and registered users differ in their rental patterns?
- Is temperature associated with hourly rental demand?
- How do weather conditions and working days relate to demand?
- What business decisions could be informed by these findings?

### Dataset

The analysis uses `hour.csv`, containing 17,379 hourly observations across 2011 and 2012.

Each row represents bike rental activity for a particular hour on a particular date.

The dataset includes:
- **Rental information:** casual, registered, and total rental counts.
- **Time information:** year, month, season, hour, weekday, and working-day status.
- **Weather information:** weather situation, normalized temperature, feeling temperature, humidity, and wind speed.

Note: Temperature, feeling temperature, humidity, and wind speed are provided as normalized values rather than their original physical units.

---

## 2. Analysis Workflow

The project followed an incremental exploratory data analysis workflow.

### Step 1: Data Audit

The initial audit focused on understanding the structure, quality, and consistency of the dataset.

Activities:
- Inspected the dataset dimensions, column names, and data types.
- Identified the unit of observation.
- Checked for missing values and duplicate records.
- Reviewed variable definitions and analytical data types.
- Verified whether total rentals matched the sum of casual and registered rentals.
- Created a data dictionary to document variable descriptions, types, and measurement units.

**Key observations:**
- Dataset contains 17,379 rows and 17 columns.
- No missing values or duplicate records were identified.
- Total rentals (`cnt`) consistently matched `casual + registered`.
- Several integer columns, such as season, hour, and weather situation, represent categorical variables rather than continuous numerical measurements.

### Step 2: Descriptive Statistics

Calculated descriptive statistics to understand the distribution and variability of rental demand.

Activities:
- Examined mean, median, standard deviation, minimum, maximum, and quartiles.
- Compared absolute and relative variability using standard deviation and coefficient of variation.
- Calculated skewness to understand distribution asymmetry.
- Examined demand percentiles to understand higher-demand hours.

**Key observations:**
- Mean rental counts were higher than median rental counts for casual, registered, and total rentals.
- All three rental variables showed positive skewness.
- Casual rentals had higher relative variability, while registered rentals had higher absolute standard deviation.
- High-demand observations contributed to the long right tail of the rental distributions.

### Step 3: Distribution Analysis

Used histograms, box plots, and violin plots to examine the distribution of hourly rental counts.

Activities:
- Visualized the distribution of total hourly rentals using a histogram.
- Used a box plot to examine the median, interquartile range, and potential outliers.
- Applied the 1.5 × IQR rule to identify potential outliers.
- Compared casual and registered rental distributions using a violin plot.

**Key observations:**
- Hourly rental counts are positively skewed.
- The median total hourly rental count is 142.
- The interquartile range is 241 rentals.
- Observations above 642.5 rentals fall beyond the upper IQR boundary and are classified as potential outliers.
- Registered users have a higher median rental count and greater absolute spread.
- Casual users have higher relative variability.

Potential outliers were treated as observations requiring investigation rather than automatically being classified as erroneous records.

### Step 4: Time-Based Demand Analysis

Examined how rental demand changes throughout the day and compared the hourly profiles of casual and registered users.

Activities:
- Calculated average rentals by hour.
- Compared hourly rental patterns across customer segments.
- Visualized average demand using line and bar charts.

**Key observations:**
- Total hourly demand has two prominent peaks: approximately 8 AM and 5 PM.
- The evening peak at 5 PM is the highest.
- Registered users show more pronounced morning and evening peaks.
- Casual users have a comparatively smoother hourly demand profile.
- Both customer segments experience their highest average hourly demand around 5 PM.

### Step 5: Temperature and Rental Demand

Investigated the relationship between temperature and rental demand.

Activities:
- Used hexagonal binning to visualize the relationship between normalized temperature and total rentals.
- Calculated Pearson and Spearman correlation coefficients.
- Compared temperature associations across casual and registered users.

**Key observations:**
- Temperature has a moderate positive association with total hourly rentals.
- Both casual and registered users show positive associations with temperature.
- The association appears stronger for casual users than for registered users.

Correlation indicates association, not causation. Other factors may also influence rental demand.

### Step 6: Weather and Working-Day Analysis

Examined how weather conditions and working-day status relate to rental demand.

Activities:
- Created contingency tables to understand the frequency of weather observations.
- Used row-normalized proportions to compare weather distributions across working and non-working days.
- Created pivot tables to calculate average hourly rentals by weather situation and working-day status.
- Visualized the results using grouped bar charts.

**Key observations:**
- Clear weather conditions are associated with the highest average hourly rental demand.
- Average demand generally decreases as weather conditions worsen.
- Working days show higher average hourly rental counts than non-working days across the observed weather categories.
- Heavy rain/snow observations are extremely limited, so comparisons involving this category should be interpreted cautiously.

---

## 3. Key Findings and Conclusion

The exploratory analysis revealed several patterns in bike-sharing demand:

1. **Time of day matters:** Rental demand has prominent morning and evening peaks, with the highest average demand around 5 PM.

2. **Customer segments behave differently:** Registered users show stronger morning and evening peaks, while casual users have a smoother hourly rental profile.

3. **Registered users have higher typical demand:** Their median hourly rental count and absolute variability are higher than those of casual users. However, casual rentals have greater relative variability.

4. **Temperature is positively associated with demand:** Both customer segments show a moderate positive relationship, with a stronger association for casual users.

5. **Weather conditions are associated with demand:** Clear weather corresponds to higher average rentals, while demand generally decreases under less favourable weather conditions.

Overall, the analysis suggests that bike-sharing demand is influenced by a combination of time-related patterns, customer behaviour, and weather conditions.

These findings provide a starting point for operational planning and further statistical modelling. However, this is an exploratory analysis, and the observed relationships should not be interpreted as causal effects.

---

## 4. Business Recommendations

Based on the findings, the following business opportunities could be explored:

| Business area | Recommendation |
|---|---|
| Fleet management | Prioritize fleet availability around 8 AM and 5 PM, paying particular attention to the registered-user morning peak and the evening peak shared by both segments. |
| Customer retention | Explore loyalty programmes, usage-based rewards, and monthly membership incentives to encourage continued engagement among registered users. |
| Customer acquisition | Investigate marketing opportunities for casual users, particularly through tourism-related campaigns and recreational usage offers. |
| Demand forecasting | Consider hour, working-day status, weather, temperature, and season as candidate features for a demand forecasting model. |

These are recommendations for further investigation, not proven interventions. For example, determining the right number of bikes to allocate requires additional information about station-level demand, fleet capacity, and bike availability.

---

## 5. Further Analysis Projects

The current dataset offers opportunities to explore several additional questions and develop more advanced analytics projects.

### 1. Bike Rental Demand Forecasting

**Objective:** Predict hourly bike rental demand using historical rental patterns and environmental variables.

Potential approaches:
- Linear and multiple regression.
- Decision trees and random forests.
- Gradient boosting models.
- Time-based train/test splits and model evaluation.

Potential features:
- Hour, weekday, month, and season.
- Working-day and holiday status.
- Temperature, humidity, wind speed, and weather situation.
- Historical rental counts and lagged demand.

### 2. Seasonal and Monthly Demand Analysis

**Objective:** Understand how bike rental demand changes across seasons and months.

Potential analysis:
- Compare average demand across seasons.
- Examine monthly and year-over-year trends.
- Identify seasonal differences between casual and registered users.
- Investigate whether seasonal patterns are consistent across years.

### 3. Customer Segmentation

**Objective:** Develop a deeper understanding of casual and registered customer behaviour.

Potential analysis:
- Compare rental patterns by hour, weekday, and season.
- Examine differences in demand sensitivity to weather.
- Explore customer usage patterns and potential membership conversion opportunities.

### 4. Tourism and Casual User Demand

**Objective:** Investigate whether tourism patterns could explain variations in casual bike rentals.

Potential data sources:
- Chicago tourism and visitor statistics.
- Visitor origin and seasonal travel data.
- Public transportation and recreational activity data.

This would require additional datasets because the current bike-sharing dataset does not identify customers' locations of origin or distinguish tourists from local casual users.

### 5. Statistical Hypothesis Testing

**Objective:** Move beyond visual comparisons and investigate whether observed differences are statistically supported.

Potential questions:
- Is average hourly demand significantly different between working and non-working days?
- Does average demand differ across weather conditions?
- Are casual and registered rental patterns significantly different across hours?
- Is the relationship between temperature and demand different between customer segments?

Possible methods include t-tests, ANOVA, non-parametric tests, and appropriate correlation comparisons, depending on the assumptions and research question.

---

## 6. Tools and Technologies

- Python
- Pandas and NumPy
- Matplotlib and Seaborn
- SciPy
- Jupyter Notebook
- Git and GitHub

## 7. Repository Structure

```text
practical-statistics-data-science/
│
├── chapter-01-eda/
│   ├── data/
│   ├── notebooks/
│   │   └── 01_data_audit.ipynb
│   ├── data_dictionary.yaml
│   └── README.md
│
├── README.md
├── requirements.txt
└── .gitignore
```

The raw dataset is kept locally and excluded from Git commits.

## 8. Reproducing the Analysis

1. Clone this repository.
2. Install the required Python packages using `pip install -r requirements.txt`.
3. Download the Bike Sharing Dataset from the [UCI Machine Learning Repository](https://archive.ics.uci.edu/dataset/275/bike+sharing+dataset).
4. Place `hour.csv` inside `chapter-01-eda/data/`.
5. Open the notebook `chapter-01-eda/notebooks/01_data_audit.ipynb` in Jupyter Notebook or VS Code.
6. Run the notebook cells sequentially.

---

*This project is part of my hands-on learning journey through Practical Statistics for Data Scientists. The goal is to apply statistical concepts to real-world datasets and translate analytical findings into meaningful business insights.*