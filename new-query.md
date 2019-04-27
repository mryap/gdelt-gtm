### To Be Executed

~~~
SELECT Actor1CountryCode country, PARSE_UTC_USEC(STRING(SQLDATE)) date, COUNT(*) c
FROM [gdelt-bq:full.events_partitioned]
WHERE Actor1CountryCode IS NOT null AND Actor1CountryCode = "GTM" 
GROUP BY 1, 2
~~~

### Partioned Table
~~~
WHERE _PARTITIONTIME
BETWEEN
TIMESTAMP(“20160101”)
 AND TIMESTAMP(“20160131”)
~~~
