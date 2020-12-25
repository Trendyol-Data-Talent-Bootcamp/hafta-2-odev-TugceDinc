# Soru 3) "sample.pageview": tablosunda 1 gün içerisinde trendyol.com a gelen tüm ziyaretlerin logu var.

```SQL
SELECT
    TIMESTAMP(date(pv.view_ts) || ' '|| EXTRACT(hour FROM view_ts) ||':'|| EXTRACT(minute FROM view_ts)||':'||'00') as dttime,
    COUNT(pv.deviceid) AS cnt
FROM tugce_dinc.pageview pv
WHERE pv.view_ts
BETWEEN
    TIMESTAMP_ADD(TIMESTAMP(date(pv.view_ts) || ' '|| EXTRACT(hour FROM view_ts) ||':'|| EXTRACT(minute FROM view_ts)||':'||'00'), INTERVAL -5 MINUTE)  and
    TIMESTAMP(date(pv.view_ts) ||' '|| EXTRACT(hour FROM view_ts) ||':'|| EXTRACT(minute FROM view_ts)||':'||'00')
GROUP BY dttime
ORDER BY dttime
```
