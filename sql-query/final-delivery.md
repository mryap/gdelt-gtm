~~~
SELECT
  STRING(MonthYear) MonthYear,
  INTEGER(norm*100000)/1000 Intensity
FROM (
  SELECT
    ActionGeo_CountryCode,
    QuadClass,
    MonthYear,
    COUNT(1) AS c,
    RATIO_TO_REPORT(c) OVER(PARTITION BY MonthYear ORDER BY c DESC) norm
  FROM
    [gdelt-bq:full.events]
  GROUP BY
    ActionGeo_CountryCode,
    QuadClass,
    MonthYear )
WHERE
  SQLDATE>=20140101
  AND SQLDATE<=20181231 AND ActionGeo_CountryCode='GT'
  AND QuadClass=4
ORDER BY
  ActionGeo_CountryCode,
  QuadClass,
  MonthYear;

~~~

~~~
SELECT
  DocumentIdentifier
FROM
  [gdelt-bq:gdeltv2.gkg]
WHERE
  V2Themes CONTAINS [
  'DISCRIMINATION',
  'UNGP_CLIMATE_CHANGE_ACTION',
  'WB_2936_GOLD',
  'WB_1700_NONMETALLIC_MINERAL_MINING_AND_QUARRYING',
  'WB_1699_METAL_ORE_MINING',
  'ENV_METALS']
  AND DATE>=20140101000000
  AND DATE<=20181231999999
  AND V2Locations LIKE '%guatemala%'
 ~~~ 

### FINAL Combin Events Eventmentions gkg
Both the Event dataset and the Global Knowledge Graph set and the API set

[Query Links](https://bigquery.cloud.google.com/savedquery/955477384685:67145645350b49bf8451932dc5c4876f)

###

~~~
SELECT
  Actor1Code,
  MonthYear,
  COUNT(GLOBALEVENTID) AS count
FROM
  [gdelt-bq:full.events_partitioned]   
WHERE
  (EventRootCode == "03"
    OR EventRootCode == "04"
    OR EventRootCode == "05"
    OR EventRootCode == "06")
  AND (Actor1Code == "NAM"
    OR Actor1Code == "MEA"
    OR Actor1Code == "CAS"
    OR Actor1Code == "SEA"
    OR Actor1Code == "AFR"
    OR Actor1Code == "ASA"
    OR Actor1Code == "EUR")
  AND (MonthYear > 201312)
GROUP BY
  MonthYear,
  Actor1Code
ORDER BY
  MonthYear DESC
~~~
