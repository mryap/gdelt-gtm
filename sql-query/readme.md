### Sql Queries that Work

Count the number of events that occurred in GTM that are hostile with Ethnic Code [Saved Query Link](https://bigquery.cloud.google.com/savedquery/955477384685:87007a0dfe024cf59618f0f89931ec2c)
~~~
SELECT
  Actor1CountryCode,
  MonthYear,
  COUNT(GLOBALEVENTID) AS count
FROM
  [gdelt-bq:full.events]
WHERE
  (EventRootCode == "01" #MAKE PUBLIC STATEMENT
    OR EventRootCode == "10" #DEMAND
    OR EventRootCode == "14" #PROTEST
    OR QuadClass =4
    )
  AND (Actor1CountryCode == "GTM")
  AND (Actor1Code == "civilians")
  AND (Actor1Code == "mnc")
  AND (Actor1EthnicCode =="mya")
  AND (Actor1EthnicCode =="xnc")
  AND (MonthYear > 201401 and MonthYear < 201812)
GROUP BY
  MonthYear,
  Actor1CountryCode
ORDER BY
  MonthYear DESC


~~~



Count the number of events that occurred in GTM that are hostile [Saved Query Link](https://bigquery.cloud.google.com/savedquery/955477384685:79fa75e784f049b79538bfa22645856a)
~~~
SELECT
  Actor1CountryCode,
  MonthYear,
  COUNT(GLOBALEVENTID) AS count
FROM
  [gdelt-bq:full.events]
WHERE
  (EventRootCode == "01" #MAKE PUBLIC STATEMENT
    OR EventRootCode == "10" #DEMAND
    OR EventRootCode == "14" #PROTEST
    OR QuadClass =4
    )
  AND (Actor1CountryCode == "GTM"
    )
  AND (MonthYear > 201401)
GROUP BY
  MonthYear,
  Actor1CountryCode
ORDER BY
  MonthYear DESC
~~~  

### Sql query (error)
https://bigquery.cloud.google.com/savedquery/955477384685:6b7fe55cdbde4df2a4402669a3d82a66

### Draft Code
~~~
SELECT
  Actor1CountryCode,
  MonthYear,
  COUNT(GLOBALEVENTID) AS count
FROM
  [gdelt-bq:full.events]
WHERE
  (EventRootCode == "01" #MAKE PUBLIC STATEMENT
    OR EventRootCode == "10" #DEMAND
    OR EventRootCode == "14" #PROTEST
    OR QuadClass =4
    )
  AND (Actor1CountryCode == "GTM"
    )
  AND (MonthYear > 201401)
GROUP BY
  MonthYear,
  Actor1Code
ORDER BY
  MonthYear DESC

~~~

~~~
#LegacySQL
SELECT Year, Target, QuadClass, COUNT(Year) AS TotalEvents FROM
(SELECT 
    Year,
    Actor2CountryCode AS Target,
    QuadClass 
  FROM [gdelt-bq:full.events]
  WHERE Actor1CountryCode = "GTM" AND Actor2CountryCode IS NOT NULL AND QuadClass =4 ), 
  (SELECT
  Year,
  Actor1CountryCode AS Target,
  QuadClass
  FROM [gdelt-bq:full.events]
  WHERE Actor2CountryCode = "GTM" AND Actor1CountryCode IS NOT NULL AND QuadClass =4
 )
GROUP BY Year, Target, QuadClass
ORDER BY Year DESC, TotalEvents DESC
~~~
