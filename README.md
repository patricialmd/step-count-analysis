## About
My mom is a senior citizen and I wanted to use her step count data to understand her daily activity patterns. So I combined her Fitbit step count data with Sydney weather data from the Australian Government Bureau of Meteorology to answer these questions:
* Does weather really affect her activity?
* Are her weekends less active?
* How much does temperature and humidity matter?
* Is her activity declining, and what can I do about it?

### **Dataset**: 393 days of step count data (Oct 2024 - Oct 2025) merged with weather variables
### **Tools Used**: Google Sheets for merging the datasets and Python for data analysis
### **Analysis**: statistical hypothesis tests and visualisations
### **Goal**: to find actionable insights to help keep her active and well as she ages.


## Data
**Step count data** tracked via my mom's Fitbit and **weather data** taken from the Australian Government Bureau of Meteorology (bom.gov.au), specifically from the Sydney weather station.
| # | Variable | Description |
|---|----------|-------------|
| **Step count data:** |
| 1 | date | Observation date |
| 2 | steps | Daily number of steps tracked from her fitness device  |
| **Weather data:** |
| 3 | min_temp | Minimum temperature (°C) for the day |
| 4 | max_temp | Maximum temperature (°C) for the day |
| 5 | rainfall | Rainfall amount (mm) for the day |
| 6 | evaporation | Evaporation (mm) for the day [removed - 100% missing] |
| 7 | sunshine | Hours of bright sunshine [removed - 100% missing] |
| 8 | wind_gust_dir | Direction of strongest wind gust |
| 9 | wind_gust_speed | Speed of strongest wind gust (km/h) |
| 10 | wind_gust_time | Time of strongest wind gust |
| 11 | temp_9am | Temperature (°C) at 9am |
| 12 | humidity_9am | Humidity (%) at 9am |
| 13 | cloud_9am | Cloud cover at 9am [removed - 100% missing] |
| 14 | wind_dir_9am | Wind direction at 9am |
| 15 | wind_speed_9am | Wind speed (km/h) at 9am |
| 16 | pressure_9am | Atmospheric pressure at 9am [removed - 100% missing] |
| 17 | temp_3pm | Temperature (°C) at 3pm |
| 18 | humidity_3pm | Humidity (%) at 3pm |
| 19 | cloud_3pm | Cloud cover at 3pm [removed - 100% missing] |
| 20 | wind_dir_3pm | Wind direction at 3pm |
| 21 | wind_speed_3pm | Wind speed (km/h) at 3pm |
| 22 | pressure_3pm | Atmospheric pressure at 3pm [removed - 100% missing] |

**Initial dataset:** 393 days × 22 variables

**Cleaned dataset:** 360 days × 16 variables 
* removed 6 columns with 100% missing values: evaporation, sunshine, cloud_9am, pressure_9am, cloud_3pm, pressure_3pm
* dropped 33 rows with nulls

  
## Key Features Created
| # | Variable | Description |
|---|----------|-------------|
| 1 | day_of_week | name of the day (Monday, Tuesday, Wednesday, Thursday, Friday, Saturday, Sunday) |
| 2 | month | month number (1 to 12) |
| 3 | season | Australian season: Summer, Autumn, Winter, Spring) |
| 4 | is_weekend | True if Saturday or Sunday, False if not |
| 5 | comfortable | 1 if weather is ideal for walking (15-25°C, no rain), 0 if not  |
| 6 | temp_range | How much the temperature changed during the day (max minus min) |
| 7 | rain_category| Rainfall grouped as No Rain, Light Rain (<5mm), or Heavy Rain (≥5mm) |
| 8 | steps_7day_avg | Average daily steps over the past 7 days |
| 9 | active_day | 1 if daily steps exceed 5,000 (activity goal met), 0 if not |
| 10 | week | Week number of the year (1-52) |

**Final dataset with added key features:** 360 days × 26 variables 


## Key Findings
**1. Does weather really affect her activity?**
* Yes, humidity has the strongest impact (r=-0.243, p<0.0001). High humidity days (>75% measured at 9am) result in 27% less activity (1,732 fewer steps)
* Warm seasons matter significantly (p<0.0001). Spring/Summer show 43% more activity than Autumn/Winter (1,998 extra steps per day)
* Rain shows a trend but not statistically significant (p=0.1099). Dry days average 538 more steps (9.9% increase)
* Wind is surprising (p=0.0117). Days with wind gusts >31 km/h show 16% higher step counts (832 more steps) - wind doesn't deter walking
* Temperature variability helps (p=0.0189). Days with larger temperature swings (>10.3°C between min and max temp) see 13% more activity (775 extra steps)
  
**2. Are her weekends less active?**
* Yes, her weekends are significantly less active (p=0.0367). Weekdays average 760 more steps (14.6% increase)
* Saturday is the worst day at 4,887 steps average
* Monday is the best day at 7,318 steps average which is 50% more than Saturday
* Day of week patterns are significant (p=0.0019), which means routine and structure drive activity more than individual choice

**3. How much does temperature and humidity matter?**
* Humidity matters most of all weather variables (r=-0.243, p<0.0001). High humidity (>75% at 9am) causes 27% reduction in activity
* Morning temperature shows positive correlation (r=0.199 with temp_9am), suggesting cooler mornings encourage walking
* Temperature range matters (p=0.0189). Days with >10.3°C variation see 13% more steps
* "Comfortable" weather doesn't guarantee activity (p=0.0611, not significant). Days with ideal conditions (15-25°C max temp, no rain) surprisingly showed fewer steps than uncomfortable days - suggesting routine matters more than perfect weather
  
**4. Seasonal and monthly patterns**
* Active day success varies dramatically by season (p=0.0001): Summer 66.7%, Spring 60.3%, Autumn 41.5%, Winter 35.9% of days reach 5,000+ steps
* Monthly differences are significant (p<0.0001). November peaks at 7,429 steps while June bottoms out at 4,405 steps - a 68% difference
* Clear seasonal divide: Oct-Feb average 6,001-7,429 steps vs Mar-Sep average 4,405-5,218 steps

**5. Critical trend:**
* Activity is declining significantly over time (ρ=-0.377, p<0.0001). Over the 360-day period, there's a consistent downward trend in daily steps requiring urgent intervention

  
## Code
See step_count_analysis_python.ipynb for full analysis including data cleaning, feature engineering, statistical hypothesis tests, and visualisations.


## Key Insights
By cleaning, analysing, and visualising the 393 rows of my mom's step count data and Sydney's climate data, here is my action plan for my Mom:

**1. FIX THE WEEKEND GAP**
-mWeekends average 760 fewer steps than weekdays (Weekdays = 5,962 steps, Weekends = 5,202 steps, difference 759 steps which is significant)
- Plan: Saturday morning walks or weekend activities that naturally involve more movement

**2. PREPARE FOR WINTER**
- Monthly averages showed June = 4,405 steps (lowest) and November = 7,429 steps (highest), significant ANOVA.
- Plan: Line up indoor alternatives before winter hits like shopping centres, home walking, or indoor exercise videos.

**3. BEAT THE HUMIDITY**
- On high humidity days (>75%), she takes about 27% fewer steps.
- Plan: Check the weather daily and have a backup indoor plan ready when humidity climbs above 75%

**4. GO EARLY**
- Morning temperature shows positive correlation (r=0.199)
- Plan: Shift walks to earlier in the day when humidity is lower and conditions are better

**5. TACKLE THE DECLINING TREND which is URGENT**
- Activity has declined significantly over 360 days (ρ=-0.377)
- First 3 months average vs last 3 months shows a clear drop
- Plan: Investigate why and implement re-engagement strategies before it gets worse


## Conclusion
In summary, my mom’s activity varies by season, day of the week, and weather conditions, and it is gradually declining. Implementing the suggested action plan can help maintain or increase her daily steps and overall activity levels.

