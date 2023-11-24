# lab 5 rozwiązania

**1. zadanie 1** 

**Pkt a**
```sql
select * from postac where rodzaj='wiking' order by wiek DESC; 
delete from postac where id_postaci in (5, 4);
```

**Pkt b**

Krok 1 usuniecia kluczy obcych
```sql
alter table walizka drop foreign key walizka_ibfk_1;
alter table przetwory drop foreign key przetwory_ibfk_1;
alter table przetwory drop foreign key przetwory_ibfk_2;
```

Krok 2 pozbycie sie atrybutu auto_increment
```sql
alter table postac change id_postaci id_postaci int;
```

Krok 3 usuniecia klucza głównego
```sql
alter table postac drop primary key;
```




**2. zadanie 2**

**Pkt a**
```sql
alter table postac add pesel char(11) first;
update postac set pesel='17763874635' + id_postaci;
alter table postac add primary key(pesel);
```

**Pkt b**
```sql
alter table postac modify rodzaj enum('wiking', 'ptak', 'kobieta', 'syrena');
```

**Pkt c**
```sql
insert into postac values('17763874644', 0, 'Getruda Nieszczera', 'syrena', '1620-04-21', 140, default, default);
```

**3. zadanie 3**

**Pkt a**
```sql
select * from postac where nazwa LIKE '%a%'; 
update postac set statek='statek1' where nazwa LIKE '%a%';
```

**Pkt b**

```sql 
select * from statek where year(data_wodowania) between 1901 and 2000
update statek set max_ladownosc = 0.7 * max_ladownosc where year(data_wodowania) between 1901 and 2000;
```
**Pkt c**
```sql
alter table postac add check (wiek < 1000);
```

**4. zadanie 4**

**Pkt a**
```sql
alter table postac modify rodzaj enum('wiking', 'ptak', 'kobieta', 'syrena', 'wąż');
insert into postac values('17763874645', 9, 'Loko', 'wąż', '1320-04-11', 440, default, default);
```

**Pkt b**
```sql
create table marynarz like postac;
show create table marynarz;
insert into marynarz select * from postac where statek is not null;
```

**Pkt c**
```sql
alter table marynarz add foreign key(statek) references statek(nazwa_statku) on delete set null;
```

**5. zadanie 5**

**Pkt a**
```sql
update postac set statek = null;
update marynarz set statek = null;
```

**Pkt b**
```sql
delete from postac where nazwa='Abi';
```

**Pkt c**
```sql
delete from statek;
```

**Pkt d** 
```sql
alter table postac drop foreign key postac_ibfk_1;
alter table marynarz drop foreign key marynarz_ibfk_1;
drop table statek;
```

**Pkt e**
```sql
create table zwierz (
id int primary key auto_increment, 
nazwa varchar(40),
wiek int);
```
**Pkt f**
```sql
insert into zwierz select id_postaci, nazwa, wiek from postac where rodzaj = ('ptak');
insert into zwierz select id_postaci, nazwa, wiek from postac where rodzaj = ('syrena');
insert into zwierz select id_postaci, nazwa, wiek from postac where rodzaj = ('wąż');
```



