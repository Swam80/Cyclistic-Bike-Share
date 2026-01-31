## Data Location
The dataset consists of 12 CSV files stored locally and prepared for analysis in Google BigQuery Sandbox.

## Data Organization
Each CSV file represents one month of bike trip data.
Each row corresponds to a single bike trip.
Each column represents an attribute of the trip, including timestamps, bike type, station information, and rider category.

## Data Source and Credibility (ROCCC)
- Reliable: Data is provided by Motivate International Inc., the operator of the Cyclistic bike-share system.
- Original: This is first-party operational data collected directly from bike usage.
- Comprehensive: Includes all recorded rides within the selected 12-month period.
- Current: Covers a recent, continuous one-year timeframe.
- Cited: The data source is publicly documented and widely used for analysis.

## Licensing, Privacy, Security, and Accessibility
- Licensing: The dataset is publicly available under an open data license permitting analysis.
- Privacy: The data is anonymized and contains no personally identifiable information.
- Security: Data will be analyzed within Google BigQuery’s managed environment.
- Accessibility: CSV format allows easy access across analytical tools.

## Data Integrity Verification Plan
Data integrity will be evaluated during the processing phase by:
- Verifying consistent column names and data types across all monthly files
- Validating that ride start timestamps occur before ride end timestamps
- Identifying missing or null values in critical fields
- Checking for duplicate ride identifiers

## Relevance to the Business Question
The dataset includes rider type, time-based fields, and ride characteristics, which directly support comparisons between casual riders and annual members.

## Known Data Limitations
- No demographic information is available
- No pricing or revenue data is included
- Individual riders cannot be tracked across multiple years
