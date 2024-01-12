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
select w.nazwa, sum(e.ilosc) from wyprawa w inner join uczestnicy u on w.id_wyprawy = u.id_wyprawy
inner join ekwipunek e on u.id_uczestnika = e.idkreatury group by w.nazwa; 
```


**2. zadanie 2**

**Pkt 2.1**
```sql
select w.nazwa, count(*) as liczba, group_concat(k.nazwa separator ' | ') as nazwy from wyprawa w
inner join uczestnicy u on w.id_wyprawy = u.id_wyprawy inner join kreatura k on u.id_uczestnika = k.idkreatury group by w.nazwa;
```

**Pkt 2.2**
```sql
select e.idwyprawy, e.idetapu, s.nazwa as nazwa_sektoru, k.nazwa as kierownik, w.data_rozpoczecia, e.kolejnosc
from etapy_wyprawy e  inner join sektor s on e.sektor = s.id_sektora inner join wyprawa w on e.idwyprawy = w.id_wyprawy
inner join kreatura k on k.idkreatury = w.kierownik order by w.data_rozpoczecia, e.kolejnosc;
```

**3. Zadanie 3**

**Pkt 3.1**
```sql
select s.nazwa, count(e.sektor) as ile_odwiedzany from etapy_wyprawy e
right join sektor s on e.sektor=s.id_sektora group by s.nazwa;
```

**Pkt 3.2**
```sql
select k.nazwa, if(count(u.id_wyprawy)=0,'nie brał udziału w wyprawie','brał udział w wyprawie') as czy_brał_udział
from kreatura k left join uczestnicy u on k.idkreatury=u.id_uczestnika group by k.nazwa;
```


**4. Zadanie 4**

**Pkt 4.1**
```sql
select w.nazwa, sum(length(ew.dziennik)) from etapy_wyprawy ew inner join wyprawa w on w.id_wyprawy=ew.idwyprawy
group by nazwa having sum(length(ew.dziennik)) < 400;
```

**Pkt 4.2**
```sql
select w.id_wyprawy, sum(e.ilosc*z.waga)/count(distinct u.id_uczestnika) as waga_ekwipunku from kreatura k 
inner join uczestnicy u on u.id_uczestnika=k.idkreatury inner join wyprawa w on u.id_wyprawy=w.id_wyprawy 
inner join ekwipunek e on e.idkreatury=k.idkreatury inner join zasob z on e.idzasobu= z.idzasobu group by w.id_wyprawy;
```


**5. Zadanie 5**

**Pkt 5.1**
```sql
select k.nazwa, w.nazwa, datediff(w.data_rozpoczecia, k.dataur) as wiek from kreatura k inner join uczestnicy u on k.idkreatury = u.id_uczestnika 
inner join wyprawa w on u.id_wyprawy = w.id_wyprawy inner join etapy_wyprawy ew on u.id_wyprawy = ew.idwyprawy where ew.sektor = 7;
```
