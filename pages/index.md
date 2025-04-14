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
```sql values
select count(*) as woonobjecten, avg(oppervlakte) as avgOppervlakte, count(distinct woning_type) as Woning_Types,
max(gemiddelde_gemeente_woz) as woz from energie.energie
```
```sql valuesPand
select min(pand_bouwjaar) as oudstePand from energie.energie where pand_bouwjaar <> 0
```

<BarChart
    data={energie_labels}
    x=energieklasse
    y=aantal
    chartAreaHeight=300
    sort=false
/>

---

<BigValue
    data={values}
    value=woonobjecten
    fmt=num0
/>
<BigValue
    data={values}
    title="Gemiddelde oppervlakte"
    value=avgOppervlakte
    fmt=num1
/>
<BigValue
    data={values}
    title="Woning types"
    value=Woning_Types
    fmt=num#
/>
<BigValue
    data={valuesPand}
    title="Bouwjaar oudste pand"
    value=oudstePand
    fmt=id
/>
<BigValue
    data={values}
    title="Gemiddelde WOZ gemeente"
    value=woz
    fmt=num0
/>

---


# More charts

<Grid cols=2>
    <DataTable data={mapWijk}
        rows=all
        totalRow=true
        title="Aantal woonobjecten per wijk"
    />
    <DimensionGrid data={dimPlaats}
        title="Dimension grid locatie/type"
        metric=sum(aantal)
        limit=all
    />
</Grid>


```sql mapWijk
select wijknaam, count(*) as aantal from energie.energie group by all
```


```sql dimPlaats
select wijknaam, buurtnaam, woning_type, energieklasse, 1 as aantal from energie.energie 
```









