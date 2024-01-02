**1. Zadanie 1**

```sql
delimiter //
CREATE TRIGGER kreatura_before_insert
BEFORE INSERT ON kreatura
FOR EACH ROW
BEGIN
	IF NEW.waga <= 0
    THEN
	  SET.waga = 1;
	END IF;
END
//
```


**2. zadanie 2**

```sql
create table archiwum_wypraw (
id_wyprawy int primary key,
nazwa varchar(200),
data_rozpoczecia date,
data_zakonczenia date,
kierownik varchar(60));

delimiter //
CREATE TRIGGER wyprawa_after_delete
AFTER DELETE ON wyprawa
FOR EACH ROW
Begin
insert into archiwum_wypraw select w.id_wyprawy, w.nazwa, w.data_rozpoczecia, w.data_zakonczenia, k.nazwa from wyprawa w
inner join kreatura k on k.idkreatury = w.kierownik where id_wyprawy=old.id_wyprawy;
END
//

# nie dokonczone, przetestuj, bedzie trigger, procedury i funkcje opuszczone, sproboj z before delete
# insert - new
# update - new old 
# delete - old
```
