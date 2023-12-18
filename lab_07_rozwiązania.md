**1. Zadanie 1** 

**Pkt 1.1**
```sql
select avg(waga) from kreatura where rodzaj ='wiking';
```

**Pkt 1.2**
```sql
select rodzaj, avg(waga), count(*) as liczba_kreatur from kreatura group by rodzaj;
```

**Pkt 1.3**
```sql
select rodzaj, avg(year(current_date)-year(dataUr)) as wiek from kreatura group by rodzaj;
```

**2. Zadanie 2**

**Pkt 2.1**
```sql
select rodzaj, sum(waga*ilosc) as laczna_waga from zasob group by rodzaj;
```

**Pkt 2.2**
```sql
select nazwa, avg(ilosc * waga) as srednia_waga from zasob where ilosc >= 4 group by nazwa having avg(ilosc * waga) > 10;
```

**Pkt 2.3**
```sql
select rodzaj, count(distinct nazwa) as ile from zasob  group by rodzaj having min(ilosc) > 1;
# w tym przypadku jeżeli jakiś rodzaj zasobu posiada nazwę z ilością 1, cały rodzaj nie jest wyświetlany

select rodzaj, count(distinct nazwa) as ile from zasob where ilosc > 1 group by rodzaj;
# w tym przypadku tylko dana nazwa się nie wlicza do ostatecznego wyniku, a sam rodzaj jest wyswietlany
```

**3. Zadanie 3**

**Pkt 3.1**
```sql
select k.nazwa, e.ilosc, e.idzasobu from kreatura k inner join ekwipunek e on k.idkreatury = e.idkreatury;
```

**Pkt 3.2**
```sql
select k.nazwa, e.ilosc, z.idzasobu, z.nazwa from kreatura k inner join ekwipunek e on k.idkreatury = e.idkreatury
inner join zasob z on z.idzasobu = e.idzasobu;
```

**Pkt 3.3**
```sql
select * from kreatura k left join ekwipunek e on k.idkreatury = e.idkreatury where e.idkreatury is null;
```

**4. Zadanie 4**

**Pkt 4.1**
```sql
select k.nazwa, k.dataur, z.nazwa, z.ilosc from kreatura k inner join ekwipunek e on k.idkreatury = e.idkreatury
inner join zasob z on e.idzasobu=z.idzasobu where k.rodzaj='wiking' and year(dataur) between 1670 and 1679;
```

**Pkt 4.2**
```sql
select k.nazwa from kreatura k inner join ekwipunek e on k.idkreatury = e.idkreatury
inner join zasob z on z.idzasobu = e.idzasobu where z.rodzaj = "jedzenie" order by k.dataur desc limit 5;
```

**Pkt 4.3**
```sql
select concat(k1.nazwa, " - ", k2.nazwa) from kreatura k1, kreatura k2 where k2.idkreatury - k1.idkreatury = 5;
```

**5. Zadanie 5**

**Pkt 5.1**
```sql
select k.rodzaj, avg(e.ilosc * z.waga) as srednia_waga from kreatura k inner join ekwipunek e on k.idkreatury = e.idkreatury
inner join zasob z on z.idzasobu = e.idzasobu where k.rodzaj not in ("malpa", "waz") and e.ilosc < 30 group by k.rodzaj;
```

**Pkt 5.2**
```sql
# Rozwiązanie 1
select 'najmlodsza' as jaka, a.maxData as data, b.nazwa, a.rodzaj from (select max(dataur) maxData, rodzaj from kreatura group by rodzaj) a,
(select nazwa, dataur from kreatura) b where a.maxData = b.dataur
union
select 'najstarsza', a.minData, b.nazwa, a.rodzaj from (select min(dataur) minData, rodzaj from kreatura group by rodzaj) a,
(select nazwa, dataur from kreatura) b where a.minData = b.dataur;

# Rozwiązanie 2, nie pokazuje dwukrotnie kreatur które są jednoczesnie najstarsze i najmlodsze
select a.nazwa, a.rodzaj, a.dataur from kreatura a, (select min(dataur) min, max(dataur) max from kreatura group by rodzaj) b 
where b.min = a.dataur or b.max=a.dataur;
```
