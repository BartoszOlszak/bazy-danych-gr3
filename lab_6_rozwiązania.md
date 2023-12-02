# Lab 06 rozwiązania
**1. Zadanie 1**

**Pkt 1.1**
```sql
create table kreatura select * from wikingowie.kreatura; 
create table zasob select * from wikingowie.zasob;
create table ekwipunek select * from wikingowie.ekwipunek;
```

**Pkt 1.2** 
```sql
select * from zasob;
```

**Pkt 1.3**
```sql
select * from zasob where rodzaj='jedzenie';
```

**Pkt 1.4**
```sql
select nazwa from kreatura where idKreatury in (1, 3, 5);
```

**2. Zadanie 2**

**Pkt 2.1**
```sql
select * from kreatura where rodzaj !='wiedzma' and udzwig >= 50;
```

**Pkt 2.1**
```sql
select * from zasob where waga between 2 and 5;
```

**Pkt 2.3** 
```sql
select * from kreatura where nazwa like '%or%' and udzwig between 30 and 70;
```

**3. zadanie 3** 

**Pkt 3.1**
```sql
select * from zasob where month(dataPozyskania) between 07 and 08;
```

**Pkt 3.2**
```sql
select * from zasob where rodzaj is not null order by waga asc;
```

**pkt 3.3**
```sql
select * from kreatura where dataur is not null order by dataUr asc limit 5;
```

**4. Zadanie 4**

**Pkt 4.1**
```sql
select distinct rodzaj from zasob where rodzaj is not null;
```

**Pkt 4.2**
```sql
select concat(nazwa,' ', rodzaj) from kreatura where rodzaj like 'wi%'; #concat() laczy wartosci
```

**Pkt 4.3**
```sql
select *, (ilosc * waga) as calkowita_waga from zasob where year(dataPozyskania) between 2000 and 2007;
```


**5. Zadanie 5**
**Pkt 5.1**
```sql
select *, (ilosc*waga*0.7) as wlasciwa_waga, (ilosc*waga*0.3) as waga_odpadkow from zasob where rodzaj='jedzenie';
```

**Pkt 5.2**
```sql
select * from zasob where rodzaj is null;
```

**Pkt 5.3**
```sql
select distinct rodzaj from zasob where nazwa like 'Ba%' or nazwa like '%a' and rodzaj is not null order by rodzaj asc;
```


