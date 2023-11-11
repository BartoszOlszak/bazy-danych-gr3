# lab 4 rozwiązania

1. **Zadanie 1**

```sql
create table postac (
id_postaci int primary key auto_increment,
nazwa varchar(40),
rodzaj enum("wiking", "ptak", "kobieta"),
data_ur date,
wiek int unsigned);
```
```sql
insert into postac values(default, "Bjorn", "wiking","1700-10-23",40);
insert into postac values(default, "Drozd", "ptak","1734-09-21",6);
insert into postac values(default, "Tesciowa", "kobieta","1656-11-22",231);
```
```sql
update postac set wiek=88 where nazwa="Tesciowa";
```
2.Zadanie 2
```sql
create table walizka (
id_walizki int primary key auto_increment,
pojemnosc int unsigned,
kolor enum("rozowy", "czerwony", "teczowy", "zolty"),
id_wlasciciela int,
foreign key(id_wlasciciela) references postac(id_postaci) on delete cascade);
```
```sql
alter table walizka alter kolor set default "rozowy"
```
```sql
insert into walizka values(default, 20, "czerwony", 1);
insert into walizka values(default, 15, default, 3);
**Listing 1** -> pogrubienie  
_Listing 2_ -> podkreślenie

**_Listing 3_**

Poniżej to blok kodu.
```sql
SELECT * FROM osoba;
```
Kod umieszczany liniowo. Polecenie `SELECT` oznacza wybranie danych z bazy.



