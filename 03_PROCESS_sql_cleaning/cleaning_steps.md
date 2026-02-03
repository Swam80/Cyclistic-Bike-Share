## Data Cleaning & Feature Engineering

Created analytical table: cyclistic_processed.trips_all_cleaned

Steps performed:

1. Removed invalid timestamps
   - Excluded rides where ended_at <= started_at since end time cannot be less than start time.
   - 29 records removed

2. Removed unrealistic ride durations (outlier handling)
   - Excluded rides < 1 minute 
   - Excluded rides > 24 hours
   - ~156k records removed (~2.7%)

3. Feature engineering
   - ride_length_minutes using TIMESTAMP_DIFF
   - day_of_week from started_at using FORMAT_TIMESTAMP
   - month extracted for seasonality analysis

Final cleaned dataset:
- Rows: 5,574,893
- Duration range: 1–1439 minutes
- Average ride length: 14.3 minutes

Now this table is ready for Analysis and BI
