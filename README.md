# GDELT

The Global Database of Events, Language, and Tone (GDELT) Event dataset which uses Google BigQuery contains a rich set of fields to describe an event that has caught media attention  http://arpieb.com/2018/06/20/digging-into-the-gdelt-event-schema/  

## Database
GDELT 2.0 in Google BigQuery: [Events](https://bigquery.cloud.google.com/table/gdelt-bq:gdeltv2.events) | [Global Knowledge Graph](https://bigquery.cloud.google.com/table/gdelt-bq:gdeltv2.gkg)| [API](https://blog.gdeltproject.org/gdelt-geo-2-0-api-debuts/)

### SQL Query 

-- This uses source as GTM meaning Guatemala. Replace it with whatever source country you want to use.

-- Run the query on Google's big query platform: https://bigquery.cloud.google.com/table/gdelt-bq:full.events?pli=1

~~~
SELECT Actor1CountryCode country, PARSE_UTC_USEC(STRING(SQLDATE)) date, COUNT(*) c
FROM [gdelt-bq:full.events]
WHERE Actor1CountryCode IS NOT null AND Actor1CountryCode = "GTM" 
GROUP BY 1, 2
~~~


https://bigquery.cloud.google.com/savedquery/92656134628:1b7c1ca7708241a5a8685bb4659ffe7a


![](https://user-images.githubusercontent.com/15719191/56752035-5240d980-677f-11e9-9b4d-4e77f96b9474.png)
