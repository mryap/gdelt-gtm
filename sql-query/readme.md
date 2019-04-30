~~~
SELECT
  Actor1Code,
  MonthYear,
  COUNT(GLOBALEVENTID) AS count
FROM
  [gdelt-bq:full.events]
WHERE
  (EventRootCode == "01" #MAKE PUBLIC STATEMENT
    OR EventRootCode == "10" #DEMAND
    OR EventRootCode == "14" #PROTEST
    OR QuadClass == "4"
    )
  AND (Actor1Code == "GTM"
    )
  AND (MonthYear > 201401)
GROUP BY
  MonthYear,
  Actor1Code
ORDER BY
  MonthYear DESC

~~~
