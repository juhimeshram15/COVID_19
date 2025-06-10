This project builds ETL pipeline using Aws glue processing daily covid-19 reports (01.01.2021,01.01.2022,01.01.2023)
GOAL:
  - Merge daily CSVs
  - Normalize countries
  - Calculate new daily cases
  -  Add 7-day moving averages
  - Clean and filter data
  -  Output structured results for dashboard use
Tools and Purpose
  Aws glue : Pyspark and  ETL Jobs
  Glue Crawler :schema detection
  Aws s3 : for strorage of cleaned and raw data
  Parquet:cleanded data file format

ETL Flow
  Raw Input
    folder-raw
ETL Steps(In Glue):
  1. Read + merge all daily files
  2. Remove nulls and 0s where needed
  3. Calculate:
   - `New_Cases = confirmed - previous_day_confirmed`
   - `New_Cases_MA7 = 7-day moving avg of New_Cases`
  4. Round metrics like `case_fatality_ratio`
  5. Output clean Parquet file to `S3/processed/`
