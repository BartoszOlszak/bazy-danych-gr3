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




**2. zadanie 2 

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
```
insert into postac values('17763874644', 0, 'Getruda Nieszczera', 'syrena', '1620-04-21', 140, default, default);
```

