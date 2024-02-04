# SQL-assignment
QUESTION 1 : What are the total number of bike stations in Austin?
```sql
SELECT
  COUNT(station_id) AS total_stations
FROM
  `bigquery-public-data.austin_bikeshare.bikeshare_stations`;
```
![q9](https://github.com/varshanbhag06/SQL/assets/153843798/d48b8593-a462-4a19-a464-04107c468ec8)
