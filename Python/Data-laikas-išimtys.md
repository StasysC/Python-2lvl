# Kaip patikrinti kintamojo tipą (funkcija type):
```python
sarasas = ["Vienas", "Du", "Trys"]
skaicius = 123
kablelis = 5.56
zodynas = {"Mantas": 20}
loginis = True
print(type(sarasas))
print(type(skaicius))
print(type(kablelis))
print(type(zodynas))
print(type(loginis))

# <class 'list'>
# <class 'int'>
# <class 'float'>
# <class 'dict'>
# <class 'bool'>
```
Programa, kuri paskaičiuoja ir atspausdina sąrašo skaičių (sveikų) sumą:
```python
sarasas = [5, 8, "Lietuva", 95, "Žodis", True]

suma = 0

for x in sarasas:
    if type(x) is int:
        suma += x

print(suma)

# 108
```
# Data, laikas (Datetime)
Datetime kintamasis gali išsaugoti datą ir/arba laiką. Jis importuojamas per import datetime

Dabartinė data ir laikas:
```python
import datetime

x = datetime.datetime.today()
print(x)

# 2020-11-25 12:41:47.651313
```
Tik data:
```python
import datetime

x = datetime.date.today()
print(x)

# 2020-11-25
```
Tik laikas:
```python
import datetime

x = datetime.datetime.today().time()
print(x)

# 12:43:45.571871
```
```python
import datetime
y = datetime.datetime(2020, 2, 29, 18, 20, 50)
print(y)
# 2020-02-29 18:20:50

print(y.strftime("%A, %d. %B %Y %I:%M%p"))
# Saturday, 29. February 2020 06:20PM
```
Datetime formatavimo kodai: https://www.w3schools.com/python/python_datetime.asp


# Kaip pridėti ar atimti laiką:
```python
import datetime
now = datetime.datetime.now()
print(now)
print(now - datetime.timedelta(days=5))
print(now + datetime.timedelta(hours=5))
print(now + datetime.timedelta(days=20, hours=8))

# 2020-11-25 12:26:14.575023
# 2020-11-20 12:26:14.575023
# 2020-11-25 17:26:14.575023
# 2020-12-15 20:26:14.575023
```
# Kaip sužinoti datų skirtumą (pvz. dienomis):
```python
import datetime
now = datetime.datetime.now()
nepriklausomybes_diena = datetime.datetime(1990, 3, 11)
skirtumas = now - nepriklausomybes_diena
print(skirtumas.days)

# 10590
```
# Kaip įvesti datą/laiką:
```python
import datetime
ivesta_data = input("Įveskite datą: ")
data = datetime.datetime.strptime(ivesta_data, "%Y-%m-%d %H:%M:%S")
skirtumas = (datetime.datetime.now() - data)
print(skirtumas.days)

# Įveskite datą: 2004-03-29 00:00:00
# 5604
```
# Kaip iš datetime atskirai ištraukti metus, mėnesį, valandas...?
```python
import datetime

now = datetime.datetime.today()

print(now.year)
print(now.month)
print(now.weekday())
print(now.day)
print(now.hour)
print(now.minute)
print(now.second)
print(now.microsecond)

# 2020
# 11
# 2
# 25
# 12
# 13
# 45
# 760594
```
Naudodami timedelta galime pamatuoti, per kiek laiko mūsų kompiuteris susidorojo su užduotimi, pvz.:
```python
import datetime

pradzia = datetime.datetime.today()
for x in range(1000000):
    print("Labas")

pabaiga = datetime.datetime.today()
print(f"Programa užtruko {(pabaiga - pradzia).total_seconds()}")
```
Taip pat galime į kodą įdėti pauzę:
```python
import time

for x in range(1000000):
    print("Labas")
    time.sleep(2)
```

# Kuo naudingas try/except/finally naudojimas:
* Leidžia pakeisti klaidų pranešimus norimu tekstu
* Įvykus klaidai, programa nesustoja (apsaugo nuo lūžimo). Po neįvykdyto kodo, programa vykdoma toliau
* Leidžia nuspręsti, ką daryti, atsiradus klaidai (pvz., išmesti tam tikrą pranešimą, paleisti kitą funkciją ir t.t
  
# Išimtys, jų suvaldymas (su try/except/finally):
```python
7 / 0
# ZeroDivisionError: division by zero


skaicius = int(input("Įveskite skaičių: "))
# Įveskite skaičių: k11
# ValueError: invalid literal for int() with base 10: 'k11'
```
Ką daryti, kad programa išmestų norimą pranešimą ir nesustotų? Variantas:
```python
dalinys = 7
daliklis = 0
if daliklis == 0:
    print("Dalyba iš nulio negalima")
else:
    dalinys / daliklis
print("Programa vykdoma toliau")

# Dalyba iš nulio negalima
# Programa vykdoma toliau
```
# Klaidų suvaldymas naudojant try/except:
```python
try:
    7 / 0
except:
    print("Dalyba iš nulio negalima")
    
# Dalyba iš nulio negalima


try:
    skaicius = int(input("Įveskite skaičių: "))
except:
    print("Įvestas klaidingas skaičius")
    
# Įveskite skaičių: k11
# Įvestas klaidingas skaičius


try:
    open('file.txt')
except:
    print("Nepavyksta atidaryti failo")

print("Programa vykdoma toliau")

# Nepavyksta atidaryti failo
# Programa vykdoma toliau
```
# Kaip suvaldyti kelias išimtis:
```python
try:
    skaicius = int(input("Įveskite skaičių: "))
    print(7 / skaicius)
    open('file.txt')
except ZeroDivisionError:
    print("Dalyba iš nulio negalima")
except ValueError:
    print("Įvestas klaidingas skaičius")
except FileNotFoundError:
    print("Nepavyko atidaryti failo")

# Įveskite skaičių: k11
# Įvestas klaidingas skaičius


# Įveskite skaičių: 0
# Dalyba iš nulio negalima


# Įveskite skaičių: 7
# 1.0
# Nepavyko atidaryti failo
```
Galimų klaidų sąrašas: https://docs.python.org/3/library/exceptions.html

# Finally blokas
(kodas, vykdomas nepaisant to, kas įvyksta try/except blokuose)
```python
try:
    print(7 / 0)
except:
    print("Dalyba iš nulio negalima")
finally:
    print("Todėl įvykdysime daugybą: ")
    print(7 * 7)
print("Programa vykdoma toliau")


# Dalyba iš nulio negalima
# Todėl įvykdysime daugybą:
# 49
# Programa vykdoma toliau
```
# Kaip panaudoti try/except įvedant duomenis:
```python
while True:
    try:
        x = int(input("Įveskite skaičių: "))
        break
    except ValueError:
        print("Įvedėte ne skaičių. Bandykite dar kartą")
```

# Užduotys
## 1 užduotis
Parašyti programą, kuri:

* Leistų vartotojui įvesti sveiką skaičių.
* Atspausdinti True, jei skaičius teigiamas
* Atspausdinti False, jei skaičius neigiamas ar lygus 0
* True/False reikšmei išsaugoti naudoti boolean tipo kintamąjį ar_skaicius_teigiamas

Patarimas: naudoti input, boolean

## 2 užduotis
Parašyti programą, kuri:

* Atspausdintų dabartinę datą ir laiką
* Atimtų iš dabartinės datos ir laiko 5 dienas ir juos atspausdintų
* Pridėti prie dabartinės datos ir laiko 8 valandas ir juos atspausdintų
* Atspausdintų dabartinę datą ir laiką tokiu formatu: 2019 03 08, 09:57:17

Patarimas: naudoti datetime, timedelta (from datetime import timedelta)

https://www.w3schools.com/python/python_datetime.asp

## 3 užduotis
Parašyti programą, kuri:

* Leistų vartotojui įvesti norimą datą ir laiką (pvz. gimtadienį)
* Paskaičiuotų ir atspausdintų, kiek nuo įvestos datos ir laiko praėjo:
  
Metų

Mėnesių

Dienų

Valandų

Minučių

Sekundžių


Kadangi tiksliai galima paskaičiuoti tik dienas ir sekundes, metus, mėnesius ir t.t. paskaičiuokite apytiksliai.

Patarimas: naudoti datetime, .days, .total_seconds()

Skaičių suapvalinimo pavyzdys (kurio gali prireikti šioje užduotyje):
```python
skaicius = 4.66

print(round(skaicius))
```
## 4, 5 užduotys
Pakeisti 1 ir 3 užduotis taip, kad neteisingai įvedus duomenis ar įvykus klaidoms, programos mestų norimas klaidas lietuvių kalba (panaudoti try/except)
