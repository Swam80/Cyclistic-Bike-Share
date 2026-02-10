# Cyclistic Case Study — SQL Processing Workflow

Author: Swamesh Lotlikar  
Tool: BigQuery Sandbox  
Phase: PROCESS (Data Cleaning & Preparation)

---

## Overview

This document records all SQL queries used to transform 12 months of raw Cyclistic trip data into a single analysis-ready dataset.

The objective of this workflow is to:

- Consolidate monthly files
- Validate data integrity
- Remove invalid/outlier records
- Engineer analytical features
- Produce a clean dataset for SQL analysis and Power BI dashboards

All transformations follow Google’s data analysis methodology and maintain separation between raw and processed layers.

Datasets used:
- `cyclistic_raw` → original monthly tables
- `cyclistic_processed` → transformed tables

---

## Step 1 — Row Count Validation

### Purpose
Verify each monthly table loaded correctly and contains expected records.

### Query
```sql
SELECT '2022_01' AS month, COUNT(*) AS rows FROM `cyclistic_raw.trips_2022_01`
UNION ALL
SELECT '2022_02', COUNT(*) FROM `cyclistic_raw.trips_2022_02`
UNION ALL
SELECT '2022_03', COUNT(*) FROM `cyclistic_raw.trips_2022_03`;
-- repeated for all months
```

### Why
Ensures successful ingestion and prevents silent data loss.

---

## Step 2 — Combine Monthly Tables

### Purpose
Create one master table containing all rides for scalable analysis.

### Query
```sql
CREATE OR REPLACE TABLE `cyclistic_processed.trips_all_raw` AS
SELECT * FROM `cyclistic_raw.trips_2022_01`
UNION ALL
SELECT * FROM `cyclistic_raw.trips_2022_02`
UNION ALL
SELECT * FROM `cyclistic_raw.trips_2022_03`
-- repeated for all months
;
```

### Why
- Standardizes structure
- Simplifies querying
- Enables full-year analysis
- Uses UNION ALL to preserve all records

---

## Step 3 — Data Integrity Checks

### 3.1 Invalid Duration Check

Purpose: Detect rides with impossible timestamps.

```sql
SELECT COUNT(*) AS invalid_duration_count
FROM `cyclistic_processed.trips_all_raw`
WHERE ended_at <= started_at;
```

---

### 3.2 Null Value Check

Purpose: Ensure critical fields are complete.

```sql
SELECT
  COUNTIF(ride_id IS NULL) AS null_ride_id,
  COUNTIF(started_at IS NULL) AS null_started_at,
  COUNTIF(ended_at IS NULL) AS null_ended_at,
  COUNTIF(member_casual IS NULL) AS null_member_casual,
  COUNTIF(rideable_type IS NULL) AS null_rideable_type
FROM `cyclistic_processed.trips_all_raw`;
```

---

### 3.3 Duplicate Ride Check

Purpose: Confirm each ride is unique.

```sql
SELECT
  COUNT(*) AS total_rows,
  COUNT(DISTINCT ride_id) AS distinct_ride_ids
FROM `cyclistic_processed.trips_all_raw`;
```

---

### 3.4 Category Validation

Purpose: Validate expected rider types.

```sql
SELECT member_casual, COUNT(*) AS ride_count
FROM `cyclistic_processed.trips_all_raw`
GROUP BY member_casual;
```

---

## Step 4 — Cleaning & Feature Engineering

### Purpose
Create an analysis-ready dataset by removing unrealistic records and adding useful features.

### Business Rules Applied
- Remove rides where ended_at <= started_at
- Remove rides shorter than 1 minute (test/unlock noise)
- Remove rides longer than 24 hours (system anomalies)

### Query
```sql
CREATE OR REPLACE TABLE `cyclistic_processed.trips_all_cleaned` AS
SELECT
  *,
  TIMESTAMP_DIFF(ended_at, started_at, MINUTE) AS ride_length_minutes,
  FORMAT_TIMESTAMP('%A', started_at) AS day_of_week,
  EXTRACT(MONTH FROM started_at) AS month
FROM `cyclistic_processed.trips_all_raw`
WHERE ended_at > started_at
  AND TIMESTAMP_DIFF(ended_at, started_at, MINUTE) >= 1
  AND TIMESTAMP_DIFF(ended_at, started_at, MINUTE) <= 1440;
```

---

## Step 5 — Post-Clean Validation

### Purpose
Confirm cleaning and transformations worked correctly.

```sql
SELECT
  COUNT(*) AS rows,
  MIN(ride_length_minutes) AS min_length,
  MAX(ride_length_minutes) AS max_length,
  AVG(ride_length_minutes) AS avg_length
FROM `cyclistic_processed.trips_all_cleaned`;
```

---

## Final Dataset Summary

| Metric | Value |
|--------|---------|
| Final Rows | 5,574,893 |
| Duration Range | 1–1439 minutes |
| Average Duration | 14.3 minutes |
| Nulls in critical fields | 0 |
| Duplicate ride IDs | 0 |

---

## Outcome

The resulting table `trips_all_cleaned` is:

- Consolidated across 12 months
- Validated for integrity
- Free from invalid or unrealistic records
- Enhanced with analytical features
- Ready for behavioral analysis and dashboard creation

This table serves as the single source of truth for all downstream SQL analysis and Power BI reporting.
