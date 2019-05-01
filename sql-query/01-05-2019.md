~~~
# SQL QUERY Code https://www.youtube.com/watch?time_continue=401&v=Psp7YivWL90
SELECT
  MonthYear MonthYear,
  INTEGER(norm*100000)/1000 Percent
FROM (
  SELECT
    ActionGeo_CountryCode,
    EventRootCode,
    MonthYear,
    COUNT(1) AS c,
    RATIO_TO_REPORT(c) OVER(PARTITION BY MonthYear ORDER BY c DESC) norm
  FROM
    [gdelt-bq:full.events]
  GROUP BY
    ActionGeo_CountryCode,
    EventRootCode,
    MonthYear )
WHERE
  ActionGeo_CountryCode='GT' #https://www.gdeltproject.org/data/lookups/FIPS.country.txt
  AND EventRootCode='14' #https://www.gdeltproject.org/data/lookups/CAMEO.eventcodes.txt
ORDER BY
  ActionGeo_CountryCode,
  EventRootCode,
  MonthYear;      
~~~
[Query Link](https://console.cloud.google.com/bigquery?sq=955477384685:99ebbecf5e1c4a4b8e00a03d2036e52e)

---
SELECT a.name, b.name, COUNT(*) as count
FROM (FLATTEN(
SELECT GKGRECORDID, UNIQUE(REGEXP_REPLACE(SPLIT(V2Persons,';'), r',.*', '')) name
FROM [gdelt-bq:gdeltv2.gkg] 
WHERE DATE>20150201000000 and DATE < 20181231000000 and V2Locations like '%Guatemala%'
,name)) a
JOIN EACH (
SELECT GKGRECORDID, UNIQUE(REGEXP_REPLACE(SPLIT(V2Persons,';'), r',.*', '')) name
FROM [gdelt-bq:gdeltv2.gkg] 
WHERE DATE>20150201000000 and DATE < 20181231000000 and V2Locations like '%Guatemala%'
) b
ON a.GKGRECORDID=b.GKGRECORDID
WHERE a.name<b.name
GROUP EACH BY 1,2
ORDER BY 3 DESC
LIMIT 250

~~~



~~~
SELECT
  MAX(ActionGeo_Lat) AS lat,
  MAX(ActionGeo_Long) AS lng,
  COUNT(*) AS count,
  MAX(SOURCEURL) AS source,
  GROUP_CONCAT(UNIQUE(EventCode)) AS codes
FROM
  [gdelt-bq:gdeltv2.events]
WHERE
  SQLDATE>=20150201
  AND SQLDATE<=20181231
  AND ActionGeo_CountryCode='GTM'
  AND EventCode IN ('181',
    '1823',
    '192',
    '01',
    '10',
    '14')
  AND IsRootEvent = 1
  AND ActionGeo_Lat IS NOT NULL
  AND ActionGeo_Long IS NOT NULL
  AND QuadClass=4
GROUP BY
  ActionGeo_Lat,
  ActionGeo_Long
~~~

Root code: 01: MAKE PUBLIC STATEMENT
Root Code: 10: DEMAND
Root Code: 14: PROTEST
Specific code: 181: Abduct, hijack, or take hostage
Specific code: 1823: Killed by physical assault
Specific code: 192: Occupy Territory

---
### 2014 - 2015 
~~~
SELECT
  MAX(ActionGeo_Lat) AS lat,
  MAX(ActionGeo_Long) AS lng,
  COUNT(*) AS count,
  MAX(SOURCEURL) AS source,
  GROUP_CONCAT(UNIQUE(EventCode)) AS codes
FROM
  [gdelt-bq:full.events] 
WHERE
  SQLDATE>=20140101
  AND SQLDATE<=20150201
  AND ActionGeo_CountryCode='GTM'
  AND EventCode IN ('181',
    '1823',
    '192',
    '01',
    '10',
    '14')
  #AND IsRootEvent = 1
  AND ActionGeo_Lat IS NOT NULL
  AND ActionGeo_Long IS NOT NULL
  AND QuadClass=4
GROUP BY
  ActionGeo_Lat,
  ActionGeo_Long
~~~
