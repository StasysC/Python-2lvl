# Masyvai, ciklai
Masyvas (angl. Array) – tai kintamojo tipas, leidžiantis išsaugoti daug reikšmių

# Sąrašai (List):
```python
sarasas = []
skaiciai = [4, 5, 45, 95]
zodziai = ["Labas ", "vakaras, ", "Lietuva"]
visko_po_truputi = [5, 5.6, "Lietuva", [5, 6, 15], True]

print(zodziai)

# ['Labas ', 'vakaras, ', 'Lietuva']
```python
## Kaip pasiekti atskirus sąrašo įrašus:
zodziai = ["Labas ", "vakaras, ", "Lietuva"]

print(zodziai[0])
print(zodziai[2])

# Labas
# Lietuva


zodis = "Laba diena"
print(zodis[5])

# d

visko_po_truputi = [5, 5.6, "Lietuva", [5, 6, 15], True]
print(visko_po_truputi[3][1])

# 6
```
## Kaip į sąrašą pridėti duomenų:
```python
sarasas = [5, 2, 6]
sarasas.append(13)

print(sarasas)

# [5, 2, 6, 13]
```
## Kaip pakeisti ar ištrinti sąrašo įrašą:
```python
sarasas = [5, 2, 6]
sarasas[1] = 64
print(sarasas)

# [5, 64, 6]

sarasas2 = [5, 64, 6]
sarasas2.pop(1)
print(sarasas2)

# [5, 6]
```
## Kaip sužinoti sąrašo dydį:
```python
sarasas = [6, 98, 159, "zodziai", 5.55, True]
print(len(sarasas))

# 6

ilgiausias_zodis = "nebeprisikiškiakopūsteliaujantiesiems"
print(len(ilgiausias_zodis))

# 37

pats_ilgiausias_zodis = "Nebeprisivaizdotinklaraštininkaujantiesiems"
print (len(pats_ilgiausias_zodis))

# 43
```
# Žodynai (Dictionary):
```python
amzius = {"Rokas": 20, "Andrius": 34, "Laura": 25}
print(amzius)

# {'Rokas': 20, 'Andrius': 34, 'Laura': 25}
```
## Kaip pasiekti konkretų žodyno įrašą:
```python
amzius = {"Rokas": 20, "Andrius": 34, "Laura": 25}

print(amzius["Laura"])
# 25

print(amzius["Rokas"])
# 20
```
## Kaip pridėti į žodyną įrašą:
```python
automobilis = {"Gamintojas": "Tesla", "Modelis": "Model S P100D", "Metai": 2016}

automobilis["Galia"] = 588

print(automobilis)

# {'Gamintojas': 'Tesla', 'Modelis': 'Model S P100D', 'Metai': 2016, 'Galia': 588}
```
## Kaip pakeisti žodyno įrašą:
```python
automobilis = {"Gamintojas": "Tesla", "Modelis": "Model S P100D", "Metai": 2016}

automobilis["Metai"] = 2019

print(automobilis)

# {'Gamintojas': 'Tesla', 'Modelis': 'Model S P100D', 'Metai': 2019}
```
## Kaip ištrinti žodyno įrašą:
```python
automobilis = {"Gamintojas": "Tesla", "Modelis": "Model S P100D", "Metai": 2019}

automobilis.pop("Metai")

print(automobilis)

# {'Gamintojas': 'Tesla', 'Modelis': 'Model S P100D'}
```
# Ciklai
Ciklas – operacijos kartojimas (tiek, kiek reikalauja sąlyga)

Iteracija (lot. iteratio - kartojimas) – vienas operacijos pakartojimas

## For ciklai:
```python
sarasas = [45, 126, 7,"Labas", 45.45]

for saraso_irasas in sarasas:
    print(saraso_irasas)

# 45
# 126
# 7
# Labas
# 45.45
```
```python
skaiciai = [2, 6, 7, 9, 41, 4, 46, 789]
skaiciu_suma = 0

for skaicius in skaiciai:
    skaiciu_suma += skaicius

print(skaiciu_suma)

# 904
```

## Kaip iteruoti per žodyno įrašus:
```python
amzius = {"Rokas": 20, "Andrius": 34, "Laura": 25}

for irasas in amzius:
    print(irasas)

# Rokas
# Andrius
# Laura

for irasas in amzius.values():
    print(irasas)

# 20
# 34
# 25

for raktas, reiksme in amzius.items():
    print(raktas, reiksme)

# Rokas 20
# Andrius 34
# Laura 25
```
## Kaip sukti for ciklą tam tikrą kiekį kartų (funkcija range):
```python
for skaicius in range(6):
    print(skaicius)

# 0
# 1
# 2
# 3
# 4
# 5


for skaicius in range(4, 15, 2):
    print(skaicius)
    
# 4
# 6
# 8
# 10
# 12
# 14
```
## While ciklai:
Kol (while) [sąlyga], tol vykdyk ciklą
```python
a = 5

while a < 100:
    a += 5
    print(a)

# 10
# 15
# 20
# 25
# 30
# 35
# 40
# 45
# 50
# 55
# 60
# 65
# 70
# 75
# 80
# 85
# 90
# 95
# 100
```
## Begalinis ciklas (Infinite loop):
```python
while True:
    print("dar kartą")
    
# dar kartą
# dar kartą
# dar kartą
# dar kartą
# dar kartą
# dar kartą
# dar kartą
# ...
```
## Ciklo nutraukimas (break):
```python
sarasas = range(0, 10, 2)

for one in sarasas:
    print(one)
    if one == 4:
        print("Skaičius 4 yra šiame sąraše")
        break

# 0
# 2
# 4
# Skaičius 4 yra šiame sąraše
```
## Pakartojimo praleidimas (continue):
```python
for one in range(0, 6):
    if one == 3:
        continue
    print(one)

# 0
# 1
# 2
# 4
# 5
```
## Sąlyga [else] for ir while cikluose:
```python
for skaicius in range(1, 5):
    if skaicius == 10:
        break
    print(skaicius)
else:
    print("Ciklas užbaigtas")

# 1
# 2
# 3
# 4
# Ciklas užbaigtas
```
```python
sarasas = [2, 8, 45, 787, 45, 89, 45, 78, 78, 9, 4]
ieskomasis = int(input("Įveskite ieškomą skaičių"))

for x in sarasas:
    print(x)
    if x == ieskomasis:
        print("Skaičius rastas")
        break
else:
    print("Skaičius nerastas")

print("Programos pabaiga")
```
# Užduotys
## 1 užduotis
Sukurti norimą sąrašą ir žodyną ir juose:

* Atspausdinti vieną norimą įrašą
* Pridėti įrašą
* Ištrinti įrašą
* Pakeisti įrašą
  
Išbandyti kitas sąrašų ir žodynų funkcijas: clear(), index(), insert(), remove...

https://www.w3schools.com/python/python_ref_list.asp

https://www.w3schools.com/python/python_ref_dictionary.asp

## 2 užduotis
Parašyti programą, kuri:

Leistų vartotojui įvesti skaičių.
* Jei įvestas skaičius yra teigiamas, paprašyti įvesti dar vieną skaičių
* Jei įvestas skaičius neigiamas, nutraukti programą ir atspausdinti visų įvestų teigiamų skaičių sumą

Patarimas: Naudoti ciklą while, sąlygą if, break

## 3 užduotis
Sukurti programą, kuri:

Leistų vartotojui po vieną įvesti 5 žodžius
Pridėtų įvestus žodžius į sąrašą
Atspausdintų kiekvieną žodį, jo ilgį ir eilės numerį sąraše (nuo 1)
Sudėtingiau: kad programa leistų įvesti norimą žodžių kiekį

Patarimas: Naudoti sąrašą (list), ciklą for, funkcijas len ir index

## 4 užduotis
Kauliukų žaidimas

Sukurti programą, kuri:

* Sugeneruotų tris atsitiktinius skaičius nuo 1 iki 6
* Jei vienas iš šių skaičių yra 5, atspausdinti „Pralaimėjai...“
* Kitu atveju atspausdinti „Laimėjai!“

Patarimas: Naudoti while ciklą, funkciją random.randint (import random), else, break

Random skaičiaus generavimo pavyzdys:
```python
import random
print(random.randint(1, 6))
```
## 5 užduotis
Sukurti programą, kuri:

* Leistų vartotojui įvesti metus
* Atspausdintų „Keliamieji metai“, jei taip yra
* Atspausdintų „Nekeliamieji metai“, jei taip yra
## 6 užduotis
Perdaryti 5 užduoti taip, kad programa atspausdintų visus keliamuosius metus, nuo 1900 iki 2100 metų.

Keliamieji metai yra kas 4 metus, išskyrus paskutinius amžiaus metus, kurie keliamieji yra tik kas 400 metų

Patarimas: Google! :)
