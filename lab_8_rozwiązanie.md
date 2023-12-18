**1. Zadanie 1**

**Pkt 1.1**
```sql
create table uczestnicy select * from wikingowie.uczestnicy;
create table etapy_wyprawy select * from wikingowie.etapy_wyprawy;
create table sektor select * from wikingowie.sektor;
create table wyprawa select * from wikingowie.wyprawa;
```

**Pkt 1.2**
```sql
select k.nazwa from kreatura k left join uczestnicy u on k.idkreatury = u.id_uczestnika where u.id_uczestnika is null;
```

**Pkt 1.3**
```sql
select w.nazwa, sum(e.ilosc) from wyprawa w inner join uczestnicy u on w.id_wyprawy = u.id_wyprawy inner join ekwipunek e on u.id_uczestnika = e.idkreatury
group by w.nazwa; 
```


**2. zadanie 2**

**Pkt 2.1**
```sql
select w.nazwa, count(*) as liczba, group_concat(k.nazwa separator ' | ') as nazwy from wyprawa w inner join uczestnicy u on w.id_wyprawy = u.id_wyprawy
inner join kreatura k on u.id_uczestnika = k.idkreatury group by nazwa;
```

**Pkt 2.2**
```sql
select e.idwyprawy, e.idetapu, s.nazwa as nazwa_sektoru, k.nazwa as kierownik, w.data_rozpoczecia, e.kolejnosc from etapy_wyprawy e 
inner join sektor s on e.sektor = s.id_sektora inner join wyprawa w on e.idwyprawy = w.id_wyprawy
inner join kreatura k on k.idkreatury = w.kierownik order by w.data_rozpoczecia, e.kolejnosc;
```

**3. Zadanie 3**

**Pkt 3.1**
```sql

```

**Pkt 3.2**
```sql

```


**4. Zadanie 4**

**Pkt 4.1**
```sql

```

**Pkt 4.2**
```sql

```


**5. Zadanie 5**

**Pkt 5.1**
```sql

```
