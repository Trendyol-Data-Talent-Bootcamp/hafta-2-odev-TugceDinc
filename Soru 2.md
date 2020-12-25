# Soru 2) 1980’den itibaren herhangi bir spor grubunda üst üste 3 veya daha fazla madalya almış atletleri bulalım.

```sql
with athleteAndYear as(
    select
        Athlete,
        Year
    from tugce_dinc.summer_medals
    group by Athlete, Year
)
select
    m1.Athlete,
    count(Distinct m1.Year)
from tugce_dinc.summer_medals m1
where
    m1.Year >= 1980 and
    m1.Year + 4 in (
        select year
        from athleteAndYear ay
        where m1.Athlete = ay.Athlete
    ) and
    m1.Year + 8 in (
        select year
        from athleteAndYear ay
        where m1.Athlete = ay.Athlete
    )
group by  m1.Athlete order by m1.Athlete;
```
