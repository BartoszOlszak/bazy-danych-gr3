# kolokwium - max 10.5 pkt  wejsciowki - max 4.5 pkt (6*0.75) zadania repo - 4 pkt   zdaje sie od 10
# zadanie 1
# pkt 1
create table kreatura select * from wikingowie.kreatura; # jezeli wybrana baza to baza imienna, 
# create table olszak_infs.kreatura select * from kreatura    jezeli wybrana baza to wikingowie
create table zasob select * from wikingowie.zasob;
create table ekwipunek select * from wikingowie.ekwipunek;

# pkt 2 
select * from zasob;

# pkt 3 
select * from zasob where rodzaj='jedzenie';

# pkt 4
select nazwa from kreatura where idKreatury in (1, 3, 5); # nie dokonczone



# zadanie 2
# pkt 1
select * from kreatura where rodzaj !='wiedzma' and udzwig >= 50;

# pkt 2
select * from zasob where waga between 2 and 5;

# pkt 3 
select * from kreatura where nazwa like '%or%' and udzwig between 30 and 70;



# zadanie 3 
# pkt 1
select * from zasob where month(dataPozyskania) between 07 and 08;

# pkt 2
select * from zasob where rodzaj is not null order by waga asc;

# pkt 3
select * from kreatura where dataur is not null order by dataUr asc limit 5;



# zadanie 4
# pkt 1
select distinct rodzaj from zasob where rodzaj is not null;

# pkt 2
select concat(nazwa,' ', rodzaj) from kreatura where rodzaj like 'wi%'; #concat() laczy wartosci

# pkt 3
select *, (ilosc * waga) as calkowita_waga from zasob where year(dataPozyskania) between 2000 and 2007;



# zadanie 5
# pkt 1
select *, (ilosc*waga*0.7) as wlasciwa_waga, (ilosc*waga*0.3) as waga_odpadkow from zasob where rodzaj='jedzenie';

# pkt 2
select * from zasob where rodzaj is null;

# pkt 3
select distinct rodzaj from zasob where nazwa like 'Ba%' or nazwa like '%a' and rodzaj is not null order by rodzaj asc;



