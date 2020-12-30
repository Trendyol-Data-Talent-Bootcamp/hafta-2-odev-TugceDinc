# Soru 2) 1980’den itibaren herhangi bir spor grubunda üst üste 3 veya daha fazla madalya almış atletleri bulalım.

```sql
WITH
  athleteAndYear AS(
  SELECT
    Athlete,
    Year
  FROM
    tugce_dinc.summer_medals
  GROUP BY
    Athlete,
    Year )
SELECT
  m1.Athlete
FROM
  tugce_dinc.summer_medals m1
WHERE
  m1.Year >= 1980
  AND m1.Year + 4 IN (
  SELECT
    year
  FROM
    athleteAndYear ay
  WHERE
    m1.Athlete = ay.Athlete )
  AND m1.Year + 8 IN (
  SELECT
    year
  FROM
    athleteAndYear ay
  WHERE
    m1.Athlete = ay.Athlete )
GROUP BY
  m1.Athlete
ORDER BY
  m1.Athlete;
```
