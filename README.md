# SQL-assignment
QUESTION 1 : What are the total number of bike stations in Austin?
```sql
SELECT
  COUNT(station_id) AS total_stations
FROM
  `bigquery-public-data.austin_bikeshare.bikeshare_stations`;
```
![q9](https://github.com/varshanbhag06/SQL/assets/153843798/d48b8593-a462-4a19-a464-04107c468ec8)


QUESTION 2 : How many trips start at each station?
```sql
SELECT
  stations.name,
  COUNT(*) AS trip_count
FROM
  `bigquery-public-data.austin_bikeshare.bikeshare_stations` AS stations
JOIN
  `bigquery-public-data.austin_bikeshare.bikeshare_trips` AS trips
ON
  stations.station_id = trips.start_station_id
GROUP BY
  stations.name;
```
![a1](https://github.com/varshanbhag06/SQL-assignment/assets/153843798/b7d626af-f1ef-4be1-b525-0abc6d09da52)



QUESTION 3 : What are the stations with more docks than the average number of docks across all stations?
```sql
WITH
  AvgDocks AS (
  SELECT
    AVG(number_of_docks) AS avg_docks
  FROM
    `bigquery-public-data.austin_bikeshare.bikeshare_stations` )
SELECT
  s.name, s.station_id, s.city_asset_number, s.number_of_docks
FROM
  `bigquery-public-data.austin_bikeshare.bikeshare_stations` s
JOIN
  AvgDocks a
ON
  s.number_of_docks > a.avg_docks;
```
![q4](https://github.com/varshanbhag06/SQL/assets/153843798/a1eba6ca-b763-4fcb-8768-d18079374d0b)


QUESTION 4: Which are the top 5 bike stations with the highest number of docks?
```sql
SELECT
  name,
  number_of_docks
FROM
  `bigquery-public-data.austin_bikeshare.bikeshare_stations`
ORDER BY
  number_of_docks DESC
LIMIT
  5;
```
![q7](https://github.com/varshanbhag06/SQL/assets/153843798/143d7929-5358-488b-bbf5-fd01062fd8bc)


QUESTION 5 : What is the average trip duration for each station?
```sql
SELECT
  s.name AS station_name,
  AVG(t.duration_minutes) AS avg_duration
FROM
  `bigquery-public-data.austin_bikeshare.bikeshare_stations` s
JOIN
  `bigquery-public-data.austin_bikeshare.bikeshare_trips` t
ON
  s.station_id = t.start_station_id
GROUP BY
  s.name;
```
![q1](https://github.com/varshanbhag06/SQL/assets/153843798/1a1d2598-1c08-4a01-b8fd-6959581c95ed)


QUESTION 6 : What is the average trip duration in minutes for each bike type?
```sql
SELECT
  bike_type,
  AVG(duration_minutes) AS avg_duration
FROM
  `bigquery-public-data.austin_bikeshare.bikeshare_trips`
GROUP BY
  bike_type
```
![q2](https://github.com/varshanbhag06/SQL/assets/153843798/36d9f31f-dbe9-42e6-b576-3a2f70e7e04f)


QUESTION 7 : What are the 3 most common subscriber type for bike trips?
```sql
SELECT
  subscriber_type,
  COUNT(trip_id) AS trip_count
FROM
  `bigquery-public-data.austin_bikeshare.bikeshare_trips`
GROUP BY
  subscriber_type
ORDER BY
  trip_count DESC
LIMIT
  3; 
```
![q6](https://github.com/varshanbhag06/SQL/assets/153843798/d2393796-3afd-40b0-8215-8cf509126a23)


QUESTION 8 : How many trips are there for each subscriber type, and which types have more than 10000 trips?
```sql
SELECT
  subscriber_type,
  COUNT(*) AS trip_count
FROM
  `bigquery-public-data.austin_bikeshare.bikeshare_trips`
GROUP BY
  subscriber_type
HAVING
  trip_count > 10000;
```
![q11](https://github.com/varshanbhag06/SQL/assets/153843798/d0b0c28a-802c-4c5e-ba8c-ba769026169e)


QUESTION 9 : What are the top 3 stations with the highest total trip duration?
```sql
SELECT
  s.name,
  SUM(t.duration_minutes) AS total_duration
FROM
  `bigquery-public-data.austin_bikeshare.bikeshare_trips` t
JOIN
  `bigquery-public-data.austin_bikeshare.bikeshare_stations` s
ON
  t.start_station_id = s.station_id
GROUP BY
  s.name
ORDER BY
  total_duration DESC
LIMIT
  3;
```
![q3](https://github.com/varshanbhag06/SQL/assets/153843798/3f7b0712-71e7-42fc-82f5-3526b06dd9dd)


QUESTION 10 : Which is the station with the highest number of trips as a start station?
```sql
SELECT
  start_station_id,
  COUNT(trip_id) AS trip_count
FROM
  `bigquery-public-data.austin_bikeshare.bikeshare_trips`
GROUP BY
  start_station_id
ORDER BY
  trip_count DESC
LIMIT
  1;
```
![q8](https://github.com/varshanbhag06/SQL/assets/153843798/79dc259a-a4d8-4b04-ac32-710d0191cf78)


QUESTION 11 : How many trips start at each station, and what are the status and address of those stations?
```sql
WITH StationTrips AS (
  SELECT start_station_id, COUNT(*) as trip_count
  FROM `bigquery-public-data.austin_bikeshare.bikeshare_trips`
  GROUP BY start_station_id
)
SELECT
  stations.station_id,
  stations.name,
  stations.status,
  stations.address,
  trips.trip_count
FROM `bigquery-public-data.austin_bikeshare.bikeshare_stations` AS stations
JOIN StationTrips AS trips
ON stations.station_id = trips.start_station_id;
```
![q10](https://github.com/varshanbhag06/SQL/assets/153843798/1dc6d589-f923-491f-b479-7e383ea94272)




