#lab 5
#zadanie 1, pkt a
select * from postac where rodzaj='wiking' order by wiek DESC;  #asc - rosnacy desc - malejacy
delete from postac where id_postaci in (5, 4);

# pkt b
# alter table postac drop primary key; (nie dziala bo problem1)
# problem 1 - atrybut auto_increment
# alter table postac change id_postaci id_postaci int; (nie dziala bo klucz obcy)
# alter table ... change nazwa_kolumny nowa_nazwa + definicja;
# lub - alter table postac modify id_postaci int;

# krok 1 usuniecia kluczy obcych
alter table walizka drop foreign key walizka_ibfk_1;
alter table przetwory drop foreign key przetwory_ibfk_1;
alter table przetwory drop foreign key przetwory_ibfk_2;

# krok 2 pozbycie sie atrybutu auto_increment
alter table postac change id_postaci id_postaci int;

# krok 3 usuniecia klucza głównego
alter table postac drop primary key;

#show create table postac;



# zadanie 2, pkt a
# dodanie kolumny jako pierwszej na liscie kolumn w tabeli
# dodanie kolumny z nowym kluczem glownym na tabeli z danycmi
# najpierw bez klucza glownego bo nie maja wartosci, bo kolumny nie sa unikalne
alter table postac add pesel char(11) first;
update postac set pesel='17763874635' where id_postaci=1;
select * from postac;
# opcjonalnie wszystko na raz
update postac set pesel='17763874635' + id_postaci;
# pesel zamienia sie na liczbe bo id_postaci jest liczba
# dodanie primary key do tabeli postac
alter table postac add primary key(pesel);

# pkt 3 
# dodac syrena do kolumny rodzaj 
alter table postac modify rodzaj enum('wiking', 'ptak', 'kobieta', 'syrena');
# dokoncz zadanie 2 wstawienie sytenki, zrob lepszy plik, wejsciowka
