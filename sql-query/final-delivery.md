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
