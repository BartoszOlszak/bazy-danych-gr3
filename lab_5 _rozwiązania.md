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

# zadanie 3 a

select * from postac where nazwa LIKE '%a%'; # %b b% %b%  pokazuje co konczy/zaczyna/zawiera b
update postac set statek='statek1' where nazwa LIKE '%a%';

select * from postac where nazwa LIKE '_j%'; # _ oznacza 1 znak przed j

select * from postac where nazwa regexp 'a'; # .  jeden znak przed a, * wszystkie znaki przed a

select * from postac where nazwa regexp '[0-9]{1,2}-[0-9]{3}';  # cyfra od 0 do 9 jeden lub 2 razy,
# [0-9] - dowolna cyfra ze zbioru
# [a-k] - litery od a do k
# [aoiuey] - jeden ze znaków ([] - zbrór)
# {} - określenie krotności
# {n} - dokłanie n razy
# [n,m} - co najmniej n razy, nie wiecej niz m razy
# {n,} - co najmniej n razy

# zadanie 3 b

# przykład 1
select * from statek where data_wodowania >= '1901-01-01' and data_wodowania <= '2000-12-31'; 

# przykład 2 - warunek between
select * from statek where data_wodowania between '1901-01-01' and '2000-12-31';

# przyklad 3 
select * from statek where year(data_wodowania) between 1901 and 2000;

# select day(now()); zwraca biezaca godzine  month, day, hour, minute, second

update statek set max_ladownosc = 0.7 * max_ladownosc where year(data_wodowania) between 1901 and 2000;

# zadanie 3, pkt c

alter table postac modify wiek int unsigned check (wiek < 1000);
# lub alter table postac add check (wiek < 1000);

# test dzialania check
show create table postac;
update postac set wiek=1000 where nazwa='Drozd';

# zadanie 4

#pkt a
# dodac typ waz
alter table postac modify rodzaj enum('wiking', 'ptak', 'kobieta', 'syrena', 'wąż');

# dodac weza loko
select * from postac;
insert into postac values('17763874645', 9, 'Loko', 'wąż', '1320-04-11', 440, default, default);

#pkt b
# przykład 1 stworzenie tabeli na wzor innej, bez danych, z kluczme glownm, bez kluczy obcych
create table marynarz like postac;
show create table marynarz;

insert into marynarz select * from postac where statek is not null;

# przykład 2 
create table marynarz2 select id_postaci, nazwa, funkcja, statek from postac;
select * from marynarz2;

# pkt c
# dodanie klucza obcego
alter table marynarz add foreign key(statek) references statek(nazwa_statku) on delete set null;

show create table postac;

# zadanie 5

# pkt a 
update postac set statek = null;
update marynarz set statek = null;
select * from postac;
select * from marynarz;

# pkt b 
select * from postac;
delete from postac where nazwa='Abi';

# pkt c 
delete from statek;
select * from statek;

# pkt d 
alter table postac drop foreign key postac_ibfk_1;
show create table postac;
alter table marynarz drop foreign key marynarz_ibfk_1;
drop table statek;

# pkt e 
create table zwierz (
id int primary key auto_increment, 
nazwa varchar(40),
wiek int);

# pkt f
insert into zwierz select id_postaci, nazwa, wiek from postac where rodzaj = ('ptak');
insert into zwierz select id_postaci, nazwa, wiek from postac where rodzaj = ('syrena');
insert into zwierz select id_postaci, nazwa, wiek from postac where rodzaj = ('wąż');

