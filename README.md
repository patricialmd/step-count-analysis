# step-count-analysis
Exploratory data analysis examining how weather affects daily walking habits, using my mom's step count data with Python and interactive visualisations.

## Project Overview
* Analysed my mom's daily step count data over 360 days (October 2024 - October 2025) to understand how weather conditions affect her walking activity in Sydney, Australia.
* Conducted **12 statistical hypothesis tests** with 8 showing significant results (p < 0.05).
* Cleaned dataset from 393 to 360 rows by dropping 6 columns with 100% missing values and removing remaining null values.
* Engineered temporal and weather features including 7-day rolling averages, comfortable weather index (15-25°C, no rain), temperature range, and rain categories.
* Created **20 interactive Plotly visualisations** including time series dashboards, 3D scatter plots, correlation heatmaps, violin plots, and sunburst charts.
* Identified key factors affecting her activity: weekday versus weekend (14.6% difference), seasonal variation (43% difference), and humidity impact (27% reduction on high humidity days).

## Motivation
This project started from wanting to help my mom, who is in her 70s, understand her step count data and walking patterns. As she tracks her daily steps, I wanted to go beyond just looking at the numbers and help her see the bigger picture. What are the factors that actually influence her activity levels?
The simple question that drives this analysis is: does weather really affect how much my mom walks?
By combining her Fitbit walking data with Sydney weather data, I could explore practical questions that matter for her health and wellbeing: Are weekends actually less active? Do rainy days really keep her indoors? How much does temperature matter? What about humidity? Is she maintaining consistent activity levels over time?
Beyond helping my mom specifically, this analysis provides actionable insights that could be valuable for anyone interested in understanding their activity patterns, or for aged care facilities monitoring resident engagement and encouraging consistent physical activity among older adults.

## Code and Resources Used
* **Python Version:** 3.10.2
* **Packages:** pandas, numpy, scipy, matplotlib, seaborn, plotly
* **Development Environment:** Jupyter Notebook
* **Data Source:** Personal fitness tracking data combined with weather data from Sydney, Australia

## Data Collection
* The dataset combines:
  * **1. Step count data:** My mom's daily step counts tracked via her fitness device
  * **2. Weather data:** Temperature, rainfall, humidity, wind speed from Sydney weather station
* **Initial dataset:** 393 days × 22 variables
* **Final cleaned dataset**: 360 days × 16 variables (after removing columns with 100% missing values and handling remaining nulls)

## EDA
Key findings from exploratory data analysis:
* **Average daily steps:** 5,740 (std: 3,138)
* **Step distribution:** Right-skewed with range from 1,006 to 15,660 steps
* **Missing values:** 6 columns had 100% missing values (evaporation, sunshine, cloud_9am, pressure_9am, cloud_3pm, pressure_3pm) - removed
* **Remaining missing values:** rainfall (3), wind_gust_dir (6), wind_gust_speed (6), wind_gust_time (6), wind_dir_9am (21), wind_dir_3pm (5) - rows dropped
* **Outlier analysis:** No extreme outliers detected using IQR method (2.0 × IQR threshold) in step counts
* **Distribution patterns:**
  * **Rainfall:** extremely right-skewed (most days had no rain)
  * **Steps: **right-skewed but less extreme
  * **Temperature variables:** approximately normal
  * **Humidity at 9am:** bimodal distribution
* **Correlation findings:**
  * Strongest positive correlation: Temperature at 9am (r=0.199)
  * Strongest negative correlation: Morning humidity (r=-0.243)
  * Rainfall showed weak negative correlation (r=-0.102)

## Preprocessing and Feature Engineering
1. Data Cleaning
   1.1 Dropped 6 columns with 393 missing values (100% null)
   1.2 Removed rows with remaining missing values (33 rows dropped)
   1.3 Converted data types
   1.4 Stripped whitespace from column names
   1.5 Validated no duplicates remain
   1.6 Validated no extreme outliers in step counts
   1.7 Final dataset: 360 rows × 16 columns
3. Feature Engineering
   2.1 Temporal Features Created -
   day_of_week (Monday through Sunday)
   month - 1-12
   season - Summer (Dec-Feb), Autumn (Mar-May), Winter (Jun-Aug), Spring (Sep-Nov) based on Australian seasons
   is_weekend - Boolean flag for Saturday/Sunday
   week - ISO week number
   2.2 Weather Features Created
   comfortable - Binary flag for comfortable walking conditions (15-25°C, no rain)
    temp_range - Daily temperature variability (max_temp - min_temp)
    rain_category - Categorical: No Rain, Light Rain (<5mm), Heavy Rain (≥5mm)
    rainy - Binary flag for any rainfall (>0mm)
    high_wind - Binary flag for wind gusts > median (31 km/h)
    high_humidity - Binary flag for morning humidity > 75%
    warm_season - Binary flag for Spring/Summer
   2.3 Activity metrics created
   steps_7day_avg - 7-day rolling average of daily steps
   active_day - Binary flag for days with >5,000 steps (reaching activity goal)
   day_number - Days since start of tracking period (for trend analysis)
    Weekly step totals aggregated by ISO week number

## Statistical Analysis
Conducted 12 hypothesis tests to understand what factors actually affect my mom's daily step counts

## Visualisations
Created 20 interactive Plotly visualisations to explore the data 

## Analysis Interpretation
From the statistical analysis and visualizations, here are the key insights about what affects my mom's walking activity:

**What Weather Really Matters:**
Humidity is the real culprit - it has the strongest impact (r=-0.243). On humid days (>75%), she walks 1,732 fewer steps on average - that's a 27% reduction
Warm seasons are game-changers - Spring and Summer see 43% more activity than Autumn and Winter (nearly 2,000 extra steps per day)
Rain? Not as big a deal as I thought - there's a trend showing fewer steps on rainy days but it's not statistically significant
Wind is surprising - She actually walks 16% MORE on windier days, not less!

**Daily and Weekly Patterns:**
Weekdays work better - She consistently walks 760 more steps on weekdays (14.6% increase) compared to weekends
Mondays are peak days - highest average at 7,318 steps, possibly due to weekly routine/motivation
Weekends lag behind - especially Saturdays (4,887 steps), suggesting less structured activity
Temperature swings help - Days with bigger temperature differences (>10.3°C range) see 13% more activity

**Seasonal Insights:**
November is the golden month - 7,429 steps average (her best performance)
June is the struggle month - Only 4,405 steps average (68% lower than November!)
Active day success rates vary dramatically:

Summer: 66.7% of days hit 5,000+ steps
Winter: Only 35.9% of days reach the goal
Spring: 60.3% success rate
Autumn: 41.5% success rate

**The Concerning Trend:**
Activity is declining over time - Spearman correlation of ρ=-0.377 (p<0.0001)
This significant downward trend over 360 days suggests she may need renewed motivation or a change in routine
Despite seasonal ups and downs, the overall trajectory is heading down

**Practical Takeaways for My Mom:**
Focus on improving weekend activity - that's where the biggest opportunity is (760 fewer steps on average)
Winter months need extra attention - especially June (lowest at 4,405 steps). Indoor walking alternatives or shopping centre walks might help
High humidity days need a plan - since outdoor walking drops by 27% on humid days, having indoor alternatives ready is important
Keep up the weekday routine - whatever she's doing on weekdays is working well!
Address the declining trend - the data shows activity decreasing over time, so we need to implement re-engagement strategies before motivation drops further
Take advantage of good weather windows - mornings with lower humidity are ideal for longer walks

As with most data problems, the analysis raises new questions: Why are Mondays so successful? What specific activities drive weekday engagement? How can we replicate spring/summer motivation in winter? These would require further investigation and conversations with my mom about her routines!
