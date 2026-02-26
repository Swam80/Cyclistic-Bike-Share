# Cyclistic Case Study — Step 4: Analysis

---

## Objective

Analyze behavioral differences between casual riders and annual members to inform a data-driven strategy for converting casual riders into members.

Total rows analyzed: 5,574,893

---

# 4.1 Ride Duration Comparison

## Business Question
Do casual riders and members differ in ride duration behavior?

## Query

```sql
SELECT
  member_casual,
  COUNT(*) AS total_rides,
  ROUND(AVG(ride_length_minutes), 2) AS avg_ride_length,
  APPROX_QUANTILES(ride_length_minutes, 2)[OFFSET(1)] AS median_ride_length,
  MIN(ride_length_minutes) AS min_length,
  MAX(ride_length_minutes) AS max_length
FROM `cyclistic_processed.trips_all_cleaned`
GROUP BY member_casual
ORDER BY member_casual;
```

## Results Summary

| Rider Type | Total Rides | Avg Ride (min) | Median Ride (min) |
|------------|-------------|---------------|-------------------|
| Casual     | 1,953,132   | 19.29         | 11                |
| Member     | 3,621,761   | 11.62         | 8                 |

## Key Insights

- Casual riders take significantly longer rides (~66% longer on average).
- Median values confirm right-skewed distribution in both groups.
- Members generate higher total ride volume.
- Casual riders exhibit leisure-type behavior.
- Members exhibit commuter-type behavior.

---

# 4.2 Day-of-Week Usage Patterns

## Business Question
Do riders exhibit commuter vs recreational usage patterns across the week?

## Query

```sql
SELECT
  member_casual,
  day_of_week,
  COUNT(*) AS total_rides,
  ROUND(AVG(ride_length_minutes), 2) AS avg_ride_length
FROM `cyclistic_processed.trips_all_cleaned`
GROUP BY member_casual, day_of_week
ORDER BY member_casual,
  CASE day_of_week
    WHEN 'Monday' THEN 1
    WHEN 'Tuesday' THEN 2
    WHEN 'Wednesday' THEN 3
    WHEN 'Thursday' THEN 4
    WHEN 'Friday' THEN 5
    WHEN 'Saturday' THEN 6
    WHEN 'Sunday' THEN 7
  END;
```

## Key Observations

### Casual Riders
- Strong spike on Saturday and Sunday.
- Weekend rides are longer in duration.
- Midweek rides significantly lower.

### Member Riders
- High and consistent usage Monday–Friday.
- Slight decrease on weekends.
- Stable ride duration across weekdays.

## Interpretation

- Casual riders show clear weekend and recreational behavior.
- Members show structured weekday commuting behavior.
- This confirms behavioral segmentation between the two groups.

---

# 4.3 Monthly Seasonality Analysis

## Business Question
Are rider types influenced by seasonal patterns?

## Query

```sql
SELECT
  member_casual,
  month,
  COUNT(*) AS total_rides,
  ROUND(AVG(ride_length_minutes), 2) AS avg_ride_length
FROM `cyclistic_processed.trips_all_cleaned`
GROUP BY member_casual, month
ORDER BY member_casual, month;
```


## Graph

![Customer TYpe wise Seasonal Trend]()

## Key Observations

### Casual Riders
- Winter months (Jan–Feb) show very low ride counts.
- Ride volume increases sharply from March onward.
- Peak usage during June–August.
- Summer ride durations exceed 20 minutes on average.

### Member Riders
- More stable usage throughout the year.
- Moderate seasonal increase in summer.
- Winter usage remains substantial compared to casual riders.

## Interpretation

- Casual riders are highly seasonal and weather-dependent.
- Members use bikes consistently year-round.
- Casual riders likely include tourists and leisure users.
- Members likely rely on bikes for commuting and regular transport.

---

# Integrated Behavioral Insights

Across duration, weekday usage, and seasonality:

1. Casual riders:
   - Ride longer.
   - Ride primarily on weekends.
   - Show strong summer spikes.
   - Exhibit leisure/recreational behavior.

2. Members:
   - Ride shorter distances.
   - Ride consistently on weekdays.
   - Maintain year-round usage.
   - Exhibit commuter behavior.

---

# Strategic Implications

The goal is to convert casual riders into annual members.

However:

- Casual riders do not currently behave like commuters.
- Conversion messaging must reflect leisure behavior.
- Marketing efforts should focus on:
  - Summer campaigns
  - Weekend promotions
  - Cost-benefit framing for frequent seasonal users

This analysis provides data-backed behavioral segmentation to inform conversion strategy.

---

# Conclusion

The analysis phase successfully identified:

- Clear behavioral segmentation between rider types
- Strong seasonal trends among casual riders
- Weekday commuter patterns among members
- Significant ride duration differences

These findings form the foundation for dashboard development and strategic business recommendations in the Share phase.
