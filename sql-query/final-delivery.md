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