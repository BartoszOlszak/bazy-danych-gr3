select waga from kreatura;
select sum(waga) from kreatura;
select count(waga) from kreatura; # count nie liczy null
select avg(waga) from kreatura;

# **1. Zadanie 1** 

# **Pkt 1.1**
select avg(waga) from kreatura where rodzaj ='wiking';

# **Pkt 1.2**
select rodzaj, avg(waga) from kreatura group by rodzaj;

# *Pkt 1.3**
select rodzaj, avg(year(current_date)-year(dataUr)) as wiek from kreatura group by rodzaj;


# **2. Zadanie 2**

# **Pkt 2.1**
select rodzaj, sum(waga*ilosc) as laczna_waga from zasob group by rodzaj;

# **Pkt 2.2**
select nazwa, avg(ilosc * waga) as srednia_waga from zasob where ilosc >= 4 group by nazwa having sum(ilosc * waga) > 10;

# **Pkt 2.3**
select rodzaj, count(distinct nazwa) from zasob group by rodzaj having min(ilosc) > 1; # sprawdz
select * from zasob where ilosc > 1;


# **3. Zadanie 3**

# **Pkt 3.1**
select k.nazwa, k.idkreatury, e.idkreatury from kreatura k, ekwipunek e where k.idkreatury = e.idkreatury; # przyklad

select k.nazwa, e.ilosc, e.idzasobu from kreatura k inner join ekwipunek e on k.idkreatury = e.idkreatury;

# **Pkt 3.2**
select k.nazwa, e.ilosc, e.idzasobu, z.idzasobu, z.nazwa from kreatura k inner join ekwipunek e on k.idkreatury = e.idkreatury
inner join zasob z on z.idzasobu = e.idzasobu;

# **Pkt 3.3**
select * from kreatura k left join ekwipunek e on k.idkreatury = e.idkreatury where e.idkreatury is null; # poprawne

select k.idkreatury, e.idkreatury from kreatura k left join ekwipunek e on k.idkreatury = e.idkreatury;

select distinct idkreatury  from ekwipunek;
select idkreatury, nazwa from kreatura where idkreatury not in (select idkreatury from ekwipunek where idkreatury is not null);

# nie dokanczac, bez wejsciowki

# **4. Zadanie 4**

# **Pkt 4.1**
select * from kreatura natural join ekwipunek; # (automatycznie złączenie wewnętrzne) nie przydatne
