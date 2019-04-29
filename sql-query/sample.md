# Cloudvision API correlates images of protest events with news articles 

Explored Cloudvision image search API to correlate images of protest events with news articles related to protest themes:
~~~
SELECT
  MAX(DocumentIdentifier),
  ImageURL,
  GeoLandmarks,
  DATE,
  MAX(Labels)
FROM
  [gdelt-bq:gdeltv2.cloudvision]
WHERE
  GeoLandmarks <> 'null'
  AND Labels LIKE '%protest%'
  AND DocumentIdentifier IN (
  SELECT
    DocumentIdentifier
  FROM
    [gdelt-bq:gdeltv2.gkg]
  WHERE
    Themes LIKE '%VIOLENCE%VIOLENCE%')
GROUP BY
  DATE,
  Labels,
  GeoLandmarks,
  ImageURL
~~~  
