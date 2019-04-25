# gdelt-gtm
GDELT GTM

### SQL Query that Works
~~~
SELECT Actor1CountryCode country, PARSE_UTC_USEC(STRING(SQLDATE)) date, COUNT(*) c
FROM [gdelt-bq:full.events]
WHERE Actor1CountryCode IS NOT null AND Actor1CountryCode = "GTM" 
GROUP BY 1, 2
~~~

https://bigquery.cloud.google.com/savedquery/92656134628:1b7c1ca7708241a5a8685bb4659ffe7a
