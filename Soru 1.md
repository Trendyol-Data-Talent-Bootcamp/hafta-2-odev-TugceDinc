# Soru 1) 1980’den itibaren spor grubu bazında en çok madalya alan 1. 3. 5. ülkeyi bulalım.

```sql
with sportCountry as(
    select
        m.sport,
        m.Country ,
        count(m.medal) as cnt,
        row_number()  over(partition by m.Sport order by m.sport, count(m.medal) DESC) as rownum
    from tugce_dinc.summer_medals m
    where m.Year >=1980
    group by m.sport, m.Country having m.Sport is not null
    order by m.sport, cnt DESC
)

select
    Sport,
    Country
from sportCountry
where rownum in (1,3,5)
group by Sport, Country, cnt
order by Sport, cnt DESC

```
