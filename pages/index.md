# Energie gemeente Apeldoorn

Bijgaande is gebaseerd op data van de website van het [VNG](https://dego.vng.nl/?label=topo#16.5/52.087049/4.308188).

```sql energie_labels
select 
    energieklasse,
    CASE 
        WHEN energieklasse = 'A+++++' THEN 1
        WHEN energieklasse = 'A++++' THEN 2
        WHEN energieklasse = 'A+++' THEN 3
        WHEN energieklasse = 'A++' THEN 4
        WHEN energieklasse = 'A+' THEN 5
        WHEN energieklasse = 'A' THEN 6
        WHEN energieklasse = 'B' THEN 7
        WHEN energieklasse = 'C' THEN 8
        WHEN energieklasse = 'D' THEN 9
        WHEN energieklasse = 'E' THEN 10
        WHEN energieklasse = 'F' THEN 11
        WHEN energieklasse = 'G' THEN 12
        ELSE 13
    END as energieklasseSort,
    count(*) as aantal 
from energie.energie 
group by all
order by energieklasseSort
```

<BarChart
    data={energie_labels}
    x=energieklasse
    y=aantal
    chartAreaHeight=300
    sort=false
/>

# More charts
