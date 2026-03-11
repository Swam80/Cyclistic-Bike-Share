# Cyclistic Case Study — Step 5: Share (Power BI Visualization)

## Objective

The purpose of the **Share phase** is to communicate analytical insights through interactive visualizations that allow stakeholders to quickly understand behavioral differences between **casual riders** and **annual members**.

**Microsoft Power BI** was used to build a dashboard that translates SQL analysis results into visual insights for business decision-making.

---

# Visualization Tool

**Tool Used:** Microsoft Power BI  
**Dataset Connection Method:** DirectQuery

DirectQuery was chosen to connect Power BI directly to **Google BigQuery**, allowing the dashboard to query the processed dataset without importing large volumes of data locally.

### Benefits of DirectQuery

- Enables analysis on large datasets
- Ensures visuals reflect the most recent data
- Reduces memory usage in Power BI

---

# Data Model Design

To improve dashboard performance and usability, a **star-schema style data model** was created.

## Fact Table

**`trips_all_cleaned`**

This table contains ride-level transactional data including:

- `ride_id`
- `started_at`
- `ended_at`
- `ride_length_minutes`
- `member_casual`
- `bike_type`
- `day_of_week`
- `month`

---

## Dimension Tables

Additional dimension tables were created to support filtering and grouping.

### Date / Time Dimension

This dimension enables time-based analysis such as:

- Month
- Day of week
- Time-of-day

---

# Feature Engineering for Visualization

Additional fields were created in Power BI to support better segmentation and storytelling.

## Weekday vs Weekend

A calculated column was created to classify rides as:

- **Weekday**
- **Weekend**

This allows clearer visualization of **commuting vs leisure patterns**.

---

## Time-of-Day Segmentation

Rides were categorized into time segments:

- **Morning**
- **Afternoon**
- **Evening**
- **Night**

This helps reveal **daily riding patterns and peak usage periods**.


# Dashboard Preview

Below is the interactive Power BI dashboard created to analyze behavioral differences between casual riders and annual members.

## Dashboard Overview

![Cyclistic Dashboard]([images/dashboard_overview.png](https://github.com/Swam80/Cyclistic-Bike-Share/blob/main/05_Share/Overview.JPG))

## Behavioral Analysis

![Ride Analysis]([images/ride_analysis.png](https://github.com/Swam80/Cyclistic-Bike-Share/blob/main/05_Share/Behavioral_analysis.JPG))

## Conversion Prospects

![Conversion Opportunities]([images/time_patterns.png](https://github.com/Swam80/Cyclistic-Bike-Share/blob/main/05_Share/COnversion%20Opportunities.JPG))

# Key Visualization Insights

The dashboard highlights three major behavioral differences.

## 1. Ride Purpose

- Casual riders appear to use bikes primarily for **recreation and leisure**, reflected in **longer ride durations**.
- Members appear to use bikes primarily for **transportation and commuting**, reflected in **shorter but more frequent rides**.

---

## 2. Weekly Usage Behavior

- Members ride consistently during **weekdays**, suggesting **routine commuting behavior**.
- Casual riders show strong spikes on **weekends**, indicating **recreational use**.

---

## 3. Seasonal Dependence

- Casual riders are **highly dependent on warm-weather months**.
- Members ride more **consistently throughout the year**.

---


- Quickly understand rider behavior patterns
- Identify opportunities to **convert casual riders into members**
- Explore patterns interactively through filters

This visualization layer translates **complex SQL analysis into clear, actionable insights** for the marketing team.
