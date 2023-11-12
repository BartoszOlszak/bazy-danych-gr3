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
2. **Zadanie 2**
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
```
3. **Zadanie 3**

```sql
create table izba (
adres_budynku varchar(100),
nazwa_izby varchar(100),
metraz int unsigned,
wlasciciel int,
primary key(adres_budynku, nazwa_izby),
foreign key(wlasciciel) references postac(id_postaci) on delete set null);
```
```sql
ALTER TABLE izba ADD COLUMN kolor VARCHAR(20) DEFAULT "czarny" AFTER metraz;
```
```sql
insert into izba values("skandy 12", "spizarnia", 100, default, 1);
```
4. **Zadanie 4**

```sql
create table przetwory (
id_przetworu int primary key,
rok_produkcji int default 1654,
id_wykonawcy int,
zawartosc varchar(255),
dodatek varchar(50) default "papryczka chilli",
id_konsumenta int,
foreign key(id_wykonawcy) references postac(id_postaci),
foreign key(id_konsumenta) references postac(id_postaci));
```
```sql
insert into przetwory values (1, default, 1, "bigos", default, 3);
```




