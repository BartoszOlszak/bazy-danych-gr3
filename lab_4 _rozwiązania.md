# lab 4 rozwiązania

1. **Zadanie 1**

  **1.1**
```sql
create table postac (
id_postaci int primary key auto_increment,
nazwa varchar(40),
rodzaj enum("wiking", "ptak", "kobieta"),
data_ur date,
wiek int unsigned);
```

  **1.2**
```sql
insert into postac values(default, "Bjorn", "wiking","1700-10-23",40);
insert into postac values(default, "Drozd", "ptak","1734-09-21",6);
insert into postac values(default, "Tesciowa", "kobieta","1656-11-22",231);
```

  **1.3**
```sql
update postac set wiek=88 where nazwa="Tesciowa";
```

2. **Zadanie 2**

  **2.1**
```sql
create table walizka (
id_walizki int primary key auto_increment,
pojemnosc int unsigned,
kolor enum("rozowy", "czerwony", "teczowy", "zolty"),
id_wlasciciela int,
foreign key(id_wlasciciela) references postac(id_postaci) on delete cascade);
```

  **2.2**
```sql
alter table walizka alter kolor set default "rozowy";
```

  **2.3**
```sql
insert into walizka values(default, 20, "czerwony", 1);
insert into walizka values(default, 15, default, 3);
```

3. **Zadanie 3**

  **3.1**
```sql
create table izba (
adres_budynku varchar(100),
nazwa_izby varchar(100),
metraz int unsigned,
wlasciciel int,
primary key(adres_budynku, nazwa_izby),
foreign key(wlasciciel) references postac(id_postaci) on delete set null);
```

  **3.2**
```sql
ALTER TABLE izba ADD COLUMN kolor VARCHAR(20) DEFAULT "czarny" AFTER metraz;
```

  **3.3**
```sql
insert into izba values("skandy 12", "spizarnia", 100, default, 1);
```
4. **Zadanie 4**

   **4.1**
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

  **4.2**
```sql
insert into przetwory values (1, default, 1, "bigos", default, 3);
```

5. **zadanie 5**

  **5.1**
```sql
insert into postac values
(default, 'Asgard', 'wiking', '1678-08-12',340),
(default, 'Khorad', 'wiking', '1864-03-22',340),
(default, 'Abi', 'wiking', '1631-04-22',234),
(default, 'Berg', 'wiking', '1658-11-24',253),
(default, 'Finn', 'wiking', '1675-05-14',275);
```

  **5.2**
```sql
create table statek (
nazwa_statku varchar(100) primary key,
rodzaj_statku enum('mały', 'sredni', 'duzy'),
data_wodowania date,
max_ladownosc int unsigned);
```

  **5.3**
```sql
insert into statek values
('statek1', 'sredni', '1676-02-21', 120),
('statek2', 'duzy', '1676-07-25', 180);
```

  **5.4**
```sql
alter table postac add column funkcja varchar(50) after wiek;
```

  **5.5**
```sql
update postac set funkcja='kapitan' where nazwa='Bjorn';
```

  **5.6**
```sql
alter table postac add column statek varchar(100) default null;
alter table postac add foreign key(statek) references statek(nazwa_statku) on delete set null;
```

  **5.7**
```sql
update postac set statek='statek1' where nazwa='Bjorn';
update postac set statek='statek1' where nazwa='Drozd';
update postac set statek='statek1' where nazwa='Asgard';
update postac set statek='statek1' where nazwa='Khorad';
update postac set statek='statek2' where nazwa='Abi';
update postac set statek='statek2' where nazwa='Berg';
update postac set statek='statek2' where nazwa='Finn';
```

  **5.8**
```sql
delete from izba where nazwa_izby='spizarnia';
```

  **5.9**
```sql
drop table izba;
```



