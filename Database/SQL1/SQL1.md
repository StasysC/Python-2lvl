# Kas yra duomenų bazė
* Duomenų bazė – organizuotas duomenų rinkinys (lentelėse)
* Duomenų bazė yra failas, o ne programa
* Reliacinė duomenų bazėje lentelės susijusios tarpusavyje ryšiais
* Su duomenų baze komunikuojama užklausomis (taip kuriamos lentelės, stulpeliai, jų tipai, keičiami, trinami duomenys)
# Duomenų bazių pavyzdžiai
* Oracle
* MySQL
* Microsoft SQL Server
* PostgreSQL
* Microsoft Access
* SQLite

Darbui su SQLite duomenų baze (be python) naudosime programą [DB Browser for SQLite](https://sqlitebrowser.org/)

# Svarbiausios DB (SQL) užklausos
* **SELECT** sakinys naudojamas įrašams iš vienos ar daugiau lentelių atrinkti.
* **FROM** sakinyje nurodomos lentelės, iš kurių reikia išrinkti eilutes (sąryšiai gali būti nurodomi skirtingais JOIN variantais).
* **WHERE** sakinyje nurodoma sąlyga, kurią turi tenkinti grąžinamos eilutės.
* **GROUP BY** sąlygoje nurodoma, kad reikia grupuoti tam tikras eilutes. Grupuojant eilutes, dažniausiai naudojamos agregatinės funkcijos maksimalioms, vidutinėms ir panašioms reikšmėms išrinkti iš grupuotų eilučių.
* **ORDER BY** sakiniu nurodoma viena ar daugiau rikiavimo sąlygų.
* **HAVING** sakinyje nurodomas kriterijus, taikomas grupuojamoms eilutėms. HAVING raktinis žodis gali būti naudojamas tik tais atvejais, jeigu užklausoje yra GROUP BY sakinys.
* **INSERT** vartojamas naujų įrašų įterpimui į lentelę.
* **DELETE** leidžia ištrinti įrašus iš lentelės.
* **UPDATE** naudojamas pakeisti vieno ar daugiau įrašų reikšmes.
* **DISTINCT** - skirtingų reikšmių išrinkimas.
* **DROP TABLE** pašalina visą lentelę.

# Užklausos

Viena dažniausiai naudojamų SQL užklausų:

```sql
SELECT * FROM person
```
žvaigždutė reiškia 'viską', person - lentelės pavadinimas. Su ja paimama absoliučiai viskas iš lentelės.

![](select_all.png)

galima išrinkti tik stulpelius, kurie mus domina:
```sql
SELECT first_name, gender FROM person;
```

![](select_name_gender.png)

norėdami išrinkti unikalias (nepasikartojančias) reikšmes, po SELECT prirašome DISTINCT:

```sql
SELECT DISTINCT gender FROM person;
```
![](select_distinct_gender.png)

## WHERE

WHERE naudojame užklausos papildymui kokia nors sąlyga:
```sql
SELECT * FROM person WHERE gender="Female";
``` 
![](where_female.png)

kitas pavyzdys:
```sql
SELECT * FROM person WHERE date_of_birth > date('1980-01-01');
```
![](select_where_date.png)

sąlygas galima kombinuoti su OR arba AND:
```sql
SELECT * FROM person WHERE date_of_birth > date('1990-01-01') AND gender="Female";
```
![](young_female.png)

## ORDER BY

papildoma sąlyga rezultato išrūšiavimui pagal tam tikrą stulpelį:
```sql
SELECT * FROM person WHERE date_of_birth > date('1980-01-01') ORDER BY company;
```
![](order_by.png)

Gale prirašius DESC gausime atvikštinį rūšiavimą:
```sql
SELECT * FROM person WHERE date_of_birth > date('1980-01-01') ORDER BY company DESC;
```
![](order_by_desc.png)

## GROUP BY

Rezultatus galime grupuoti:

```sql
SELECT * FROM person GROUP BY gender, last_name;
```

![](group_by.png)

```sql
SELECT *
FROM person
GROUP BY last_name, first_name	
HAVING gender="Female";
```

![](having1.png)

sudėtingesnis pavyzdys:

```sql
SELECT *
FROM person
GROUP BY last_name, first_name	
HAVING date_of_birth BETWEEN date('1980-01-01') AND date('1990-01-01');
```
![](having2.png)

# Duomenų įterpimas
## INSERT

duomenų įterpimui naudojame INSERT, pvz:
```sql
INSERT INTO person VALUES("Jotautas", "Treigys", "jtr@gmail.com", "Male", date('1981-04-25'), "FTMC");
```
![](insert1.png)

galime įterpinėti tik į konkrečius stulpelius:
```sql
INSERT INTO person (first_name, last_name, gender, date_of_birth, company) VALUES ("Antanas", "Šampanas", "Male", date('1979-02-02'), "Microsoft");
```

![](insert2.png)

## UPDATE

Norėdami pakeisti įrašus, naudojame UPDATE:
```sql
UPDATE person SET email = "antanas@gmail.com" WHERE first_name = "Antanas";
```

![](update1.png)

kitas pvz.:
```sql
UPDATE person SET company = "Microsoft" WHERE date_of_birth >= date('1990-01-01') AND gender = "Female";
```

Galime pakeisti keleto stulpelių reikšmes:
```sql
UPDATE person SET first_name = "Mikrosoftas", last_name = "Mikrosoftauskas" WHERE company = "Microsoft";	
```

išrinkę viską pagal kompaniją 'Microsoft', gausime:

![](update2.png)

## DELETE

Triname su DELETE. Pvz.:
```sql
DELETE FROM person where company = "Microsoft";
```

jeigu nenurodome sąlygos, bus ištrintos visos eilutės:
```sql
DELETE FROM person;
```

jeigu norime ištrinti lentelę su visa struktūra:
```sql
DROP TABLE person;
```

## Duomenų lentelės kūrimas
```sql
CREATE TABLE darbuotojai (vardas text, pavarde text, atlyginimas integer)
```

# Užduotys
Parsisiųskite lentelę "darbuotojai.db", atsidarykite ją programoje DB Browser for SQLite ir skiltyje "Execute SQL" atlikite šias SQL užklausas:

1. Išrinkite visus duomenis iš lentelės “DARBUOTOJAI”.
2. Išrinkite visus duomenis iš stulpelio “GIMIMO_DATA” - lentelėje “DARBUOTOJAI”.
3. Išrinkite visus duomenis iš stulpelių “VARDAS”,”PAVARDĖ”, “PAREIGOS” - lentelėje “DARBUOTOJAI”.
4. Išrinkite unikalias reikšmes iš stulpelio SKYRIUS_PAVADINIMAS - lentelėje “DARBUOTOJAI”.
5. Išrinkite visus duomenis apie darbuotojus, kurie dirba Gamybos skyriuje.
6. Išrinkite duomenis, kokias pareigas užima Giedrius
7. Išrinkite visus duomenis apie darbuotojus, kurių gimimo data - 1986-09-19
8. Išrinkite darbuotojų vardus, kurių pavardės yra Sabutis
9. Išrinkite duomenis (vardą ir pavardę) apie programuotojus iš Gamybos skyriaus
10. Įterpkite į lentelę “DARBUOTOJAI” naują darbuotoją, užpildydami visus reikiamus laukus (vardą, pavardę, gimimo metus, pareigas, skyriaus pavadinimą).
11. Įterpkite į lentelę “DARBUOTOJAI” naują darbuotoją, užpildydami tik laukus (vardą, pavardę, gimimo metus). Pareigas ir skyriaus pavadinimą palikite neužpildytus.
12. Užpildykite likusius tuščius laukus “DARBUOTOJAI” lentelėje, jūsų prieš tai įterptame įraše. Priskirkite darbuotojui pareigas ir skyrių.
13. Ištrinkite lentelės “DARBUOTOJAI” įrašą, kurio gimimo data yra tokia, kurią jūs sukūrėte.
14. Įterpkite, du darbuotojus, pavarde Antanaitis kurių pareigos būtų “Programuotojas”.
15. Pakeiskite, abiejų Antanaičių pareigas į “Testuotojas” vienu sakiniu.
16. Suskaičiuokite, kiek įmonėje dirba Testuotojų.
