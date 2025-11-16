# Step Count Analysis
An analysis examining how weather affects daily walking habits, using my mom's step count data from Sydney, Australia.

## About
My mom, in her 70s, wanted to understand what influences her daily walking patterns. I combined her Fitbit data with Sydney weather data to answer these questions: 
* Does weather really affect her activity?
* Are her weekends less active?
* How much does temperature and humidity matter?

Dataset: 360 days of step count data (Oct 2024 - Oct 2025) merged with weather variables
Analysis: 12 statistical hypothesis tests, 20 interactive Plotly visualisations
Tools: Python, pandas, scipy, plotly, seaborn 

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

Initial: 393 days × 22 variables
Cleaned: 360 days × 16 variables 
* removed 6 columns with 100% missing values: evaporation, sunshine, cloud_9am, pressure_9am, cloud_3pm, pressure_3pm
* dropped 33 rows with nulls
  
## Key Features Created
| # | Variable | Description |
|---|----------|-------------|
| **Temporal Features:** |
| 1 | day_of_week | name of the day (Monday, Tuesday, Wednesday, Thursday, Friday, Saturday, Sunday) |
| 2 | month | month number (1 to 12) |
| 3 | season | Australian season: Summer, Autumn, Winter, Spring) |
| 4 | is_weekend | True if Saturday or Sunday, False if not |
| **Weather features:** |
| 5 | comfortable | 1 if weather is ideal for walking (15-25°C, no rain), 0 if not  |
| 6 | temp_range | How much the temperature changed during the day (max minus min) |
| 7 | rain_category| Rainfall grouped as No Rain, Light Rain (<5mm), or Heavy Rain (≥5mm) |
| **Activity metrics:** |
| 8 | steps_7day_avg | Average daily steps over the past 7 days |
| 9 | active_day | 1 if daily steps exceed 5,000 (activity goal met), 0 if not |
| 10 | week | Week number of the year (1-52) |

Final dataset with added key features: 360 days × 26 variables 

## Key Findings
**1. Does weather really affect activity?**
* **Yes**, **humidity** has the strongest impact (r=-0.243), causing 27% reduction (1,732 fewer steps) on high humidity days (>75%)
* Warm seasons (Spring/Summer) show 43% more activity than Autumn/Winter (nearly 2,000 extra steps per day)
* Rain shows a trend toward fewer steps but is not statistically significant
* Windier days show 16% higher step countss show 16% higher step counts
  
**2. Are weekends less active?**
* **Yes, weekends are less active.** Saturday is the worst day (4,887 steps average)
* Weekdays average 760 more steps (14.6% increase) compared to weekends
* Monday is the best day (7,318 steps average)

**3. How much does temperature and humidity matter?**
* **Humidity matters most**. There is 27% reduction in activity on high humidity days (>75%)
* Morning temperature shows positive correlation (r=0.199)
* When daily temperatures vary by more than 10.3°C, activity increases by 13%
* Comfortable weather (15-25°C, no rain) leads to more walking
  
* **4. Additional finding:**
* Activity is declining over time (ρ=-0.377, p<0.0001) - significant downward trend over 360 days
  
## Code
See step_count_analysis.ipynb for full analysis including data cleaning, feature engineering, 12 statistical hypothesis tests, and 20 interactive visualisations (time series, correlation heatmaps, 3D plots, violin plots)

## Practical Takeaways
Looking at a year of my mom's walking data revealed some surprises and gave us a clear action plan.
**Fix the weekend gap**: Weekends lag by 760 steps. We're planning Saturday morning walks or weekend activities that naturally involve more movement.

**Prepare for winter**: With June averaging just 4,405 steps, we're lining up indoor alternatives before winter hits: shopping centres, indoor tracks, or home walking videos.

**Beat the humidity**: A 27% drop on humid days is significant. Now we monitor the forecast and have a backup plan ready when humidity climbs above 75%.

**Tackle the downward trend**: The data doesn't lie: activity is declining. We need to understand why and implement strategies to reverse it before it gets worse.

**Go early**: Mornings have lower humidity and better conditions. Shifting walks to earlier in the day could make a real difference.
