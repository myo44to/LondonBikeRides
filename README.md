# London Bike Sharing — Exploratory Data Analysis

An exploratory data analysis of London's public bike-sharing system, examining how temporal patterns and environmental conditions drive hourly rental demand across a two-year period (2015–2017).

**Data Source:** [London Bike Sharing Dataset — Kaggle](https://www.kaggle.com/datasets/hmavrodiev/london-bike-sharing-dataset)

**Dashboard:** https://public.tableau.com/shared/SXFWWPP9N?:display_count=n&:origin=viz_share_link

---

## Dataset Features

| Feature | Description |
|---|---|
| `count` | Number of bike rentals in that hour |
| `temp_real_C` | Actual temperature (°C) |
| `temp_feels_like_C` | Perceived temperature accounting for wind chill and humidity (°C) |
| `humidity_percent` | Relative humidity (%) |
| `wind_speed_kph` | Wind speed (km/h) |
| `weather` | Weather condition (Clear, Scattered Clouds, Broken Clouds, Snowfall) |
| `season` | Season (Spring, Summer, Fall, Winter) |
| `is_holiday` | Whether the hour falls on a public holiday |
| `is_weekend` | Whether the hour falls on a weekend |
| `time` | Timestamp (hourly) |

---


## Analysis Overview

### 1. Data Acquisition & Preparation
- Downloaded directly from Kaggle via `kagglehub`
- Renamed columns for readability, remapped coded values (season, weather) to human-readable labels
- Engineered temporal features: year, month, day, hour, day of week, quarter, week of year
- Added 7-day and 30-day rolling averages for trend analysis
- Verified zero null values and zero duplicate timestamps

### 2. Univariate Analysis
- Descriptive statistics and distribution analysis for all numerical variables
- Histogram and KDE plots revealing right-skewed demand, bimodal feels-like temperature, and left-skewed humidity
- Boxplot analysis identifying outlier structure across all variables

### 3. Temporal Analysis
Demand examined at every time granularity, from broadest to finest:
- **All-time overview** — full time series with 7-day and 30-day moving averages
- **By year** — year-over-year growth in average hourly demand
- **By month** — clear seasonal arc peaking in summer, bottoming in winter
- **By day of month** — no systematic pattern; variation driven by day-of-week composition
- **By day of week** — weekdays outperform weekends; commuter vs. leisure usage profiles
- **By hour of day** — twin commute peaks at 08:00 and 17:00, with overnight trough near zero
- **Heatmaps** — Hour × Day of Week, Month × Year, and Hour × Month interaction effects

### 4. Weather Impact Analysis
- Temperature, humidity, wind speed each analyzed with binned averages and correlation coefficients
- Weather condition frequency and average demand compared side-by-side
- Optimal riding temperature identified (~20–25°C feels-like)

### 5. Correlation & Statistical Testing
- Correlation matrix across all numerical features
- Pairwise relationship plots (sampled for performance)
- Independent t-tests: weekday vs. weekend, holiday vs. non-holiday
- One-way ANOVA across all four seasons

---

## Key Findings

| Rank | Factor | Direction | Notes |
|---|---|---|---|
| 1 | Hour of day | — | 40x gap between peak (17:00) and trough (04:00) |
| 2 | Feels-like temperature | Positive | ~0.4 correlation; strongest continuous predictor |
| 3 | Season / Month | Positive (summer) | Summer ≈ 2x winter average demand |
| 4 | Day of week | Weekdays higher | Commute peaks flatten on weekends |
| 5 | Weather condition | Negative (bad weather) | Clear vs. Snowfall is a ~6x demand gap |
| 6 | Humidity | Negative | Partially captured by feels-like temperature |
| 7 | Wind speed | Negative | Weakest weather predictor |

*When* someone rides is driven by the clock and the commute. *Whether* they ride at all is driven by how the weather feels outside.

---

## Tools & Libraries

- **Python 3.12**
- `pandas` — data manipulation
- `numpy` — numerical operations
- `matplotlib` / `seaborn` — visualization
- `kagglehub` — dataset download
- `openpyxl` — Excel export

---

## Tableau Dashboard Link:
https://public.tableau.com/shared/SXFWWPP9N?:display_count=n&:origin=viz_share_link
