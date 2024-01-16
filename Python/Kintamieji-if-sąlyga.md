# Kintamieji (skaičiai):
## Sveikieji skaičiai – Integer (int):
```python
a = 5
print(a)
# 5

a = int(5)
print(a)
# 5

a = 7
print(a)
# 7

a = 10
print(a)
# 10

a = a - 4
print(a)
# 6
```
## Skaičiai su kableliu – float:
```python
a = 8.56
b = 5
c = a + b
print(c)
# 13.56

a = float(5)
print(a)
# 5.00
```
## Veiksmai su kintamaisiais:
```python
a = 5 + 2
print(a) 
# 7

b = 5 - 2
print(b) 
# 3

c = 5 * 2
print(c) 
# 10

b = 5 / 2
print(b) 
# 2.5
```
## Kintamųjų pavadinimų sudarymo taisyklės
Kintamųjų pavadinimai turi prasidėti raide arba pabraukimu, pvz:

* _vardas
* vardas

Likusioji kintamojo dalis gali būti sudaryta iš raidžių, skaičių ir pabraukimų:

* pirmas1
* antras_skaicius
* _e5786

Pavadinimuose svarbios didžiosios ir mažosios raidės:

* *Vardas* ir *vardas* būtų skirtingi kintamieji.

Kintamaisiais negali būti python raktiniai žodžiai:

'False', 'None', 'True', 'and', 'as', 'assert', 'async', 'await', 'break', 'class', 'continue', 'def', 'del', 'elif', 'else', 'except', 'finally', 'for', 'from', 'global', 'if', 'import', 'in', 'is', 'lambda', 'nonlocal', 'not', 'or', 'pass', 'raise', 'return', 'try', 'while', 'with', 'yield'

Python kalboje sudurtinius kintamųjų pavadinimus priimta sudarinėti taip:

first_block, vandens_temperatura

## Paprastesnis veiksmų atlikimas:
```python
a = 5
a += 2
print(a)
# 7

b = 12
b /= 3
print(b)
# 4.0
```

## Kėlimas laipsniu:
```python
a = 2**2
print(a)
# 4

b = 5**3
print(b)
# 125
```

## Sveikojo skaičiaus ir liekanos paieška (div/mod):
```python
a = 32 / 6
print(a)
# 5.333333333333333

b = 32 // 6
print(b)
# 5

c = 32 % 6
print(c)
# 2
```

## Simbolių eilutės (String) tipas:
```python
zodis1 = "Labas "
print(zodis1)
# Labas

zodis2 = str("vakaras")
print(zodis2)
# vakaras

print(zodis1 + zodis2)
# Labas vakaras
```
## Nauja eilutė:
```python
print("Labas \nvakaras")
# Labas
# vakaras
```

## Veiksmai su simbolių eilėmis (String):
![](https://github.com/StasysC/Python-2lvl/blob/master/Python/stringas.png)
```python
zodis = "Code Academy"

print(zodis[5])

# A

print(zodis[-2])

# m

print(zodis[5:12])

# Academy

print(zodis[5:])

# Academy

print(zodis[:4])

# Code

print(zodis[5:12:1])

# Academy

print(zodis[5::2])

# Aaey

print(zodis[::-1])

# ymedacA edoC

print(zodis.split())

# ['Code', 'Academy']

print(zodis.upper())

# CODE ACADEMY

print(zodis.replace('c', 'k'))

# Code Akademy

print(zodis.replace('Code', 'Music'))

# Music Academy
```
Geras būdas formuoti stringus iš kintamųjų:
a = 5

zodis = "Labas"
dar_vienas = "Šitas žodis"

print("a lygu: " + str(a) + ", žodis: " + zodis + ", dar vienas žodis – " + dar_vienas)

# Geresni variantai:

print(f'a lygu: {a}, žodis: {zodis}, dar vienas žodis - {dar_vienas}')
print("a lygu: %s, žodis: %s, dar vienas žodis - %s" % (a, zodis, dar_vienas))
print("a lygu: {}, žodis: {}, dar vienas žodis - {}".format(a, zodis, dar_vienas))
Veiksmai su skirtingais tipais (konvertavimas):
d = "Žodis "
e = 5
print(d+e)

# TypeError: can only concatenate str (not "int") to str

e = str(e)
print(d+e)

# Žodis 5

a = "250"
b = 4
print(a * b)

# ???
Kintamųjų įvedimas ir išvedimas:
String įvedimas:

a = input("Įveskite pirmą žodį ")
b = input("Įveskite antrą žodį ")
print("Jūsų sakinys: ", a + b)

# Įveskite pirmą žodį Python
# Įveskite antrą žodį programavimas
# Jūsų sakinys: Python programavimas
Integer, Float įvedimas:

a = int(input("Įveskite pirmą skaičių "))
b = int(input("Įveskite antrą skaičių "))
print("Jūsų skaičių suma: ", a + b)

# Įveskite pirmą skaičių 5
# Įveskite antrą skaičių 6
# Jūsų skaičių suma: 11

h = float(input("Įveskite skaičių "))
print(h)
Loginiai operatoriai:


Sąlyga IF (jeigu):
Jeigu (IF) [sąlyga], tuomet [veiksmas]

if 5 > 0:
    print("5 yra daugiau už 0")
# 5 yra daugiau už 0
if 5 < 0:
    print("5 yra daugiau už 0")
print("Programa baigta")

# Programa baigta
skaicius = 25
if skaicius < 100:
    print("1: Skaičius yra mažesnis už 100")
if skaicius > 10:
    print("2: Skaičius yra didesnis už 10")
if skaicius < 10:
    print("3: Skaičius yra mažesnis už 10")

# 1: Skaičius yra mažesnis už 100
# 2: Skaičius yra didesnis už 10

skaicius = 60
if skaicius < 70:
    print("Skaičius yra mažesnis už 70")
    if skaicius > 15:
        print("Skaičius yra tarp 15 ir 70")

# Skaičius yra mažesnis už 70
# Skaičius yra tarp 15 ir 70

skaicius = 10

# Skaičius yra mažesnis už 70
Sąlyga ELSE (jei ne, tuomet):
skaicius = 56
if skaicius == 50:
    print("1: Skaičius yra lygus 50")
else:
    print("2: Skaičius nelygus 50")

# 2: Skaičius nelygus 50
Sąlyga ELIF (jei sąlyga netenkinama ir jei):
skaicius = 0

if skaicius > 0:
    print("Teigiamas skaičius")
elif skaicius == 0:
    print("Nulis")
else:
    print("Neigiamas skaičius")

# Nulis
Kodo komentavimas:
Komentuota eilutė (PyCharm programoje – CTRL+/):

# Ši eilutė nebus vykdoma
Komentuota pastraipa (Doctrings):

"""
Sveiki, draugai,
Ši pastraipa nebus vykdoma.
"""
Užduotys
1 užduotis
Parašyti programą, kuri:

Leistų įvesti skaičius a ir b (int arba float)
Išvestų į ekraną „a mažesnis už b“, jei taip yra
Išvestų į ekraną „a lygu b“, jei taip yra
Išvestų į ekraną „a didesnis už b“, jei taip yra
Patarimas: naudoti if, elif, else sąlygas

2 užduotis
Parašyti programą, kuri su eilute "Zen of Python" darytų šiuos veiksmus:

Atspausdintų paskutinį antro žodžio simbolį
Atspausdintų pirmą trečio žodžio simbolį
Atspausdintų tik pirmą žodį
Atspausdintų tik paskutinį žodį
Atspausdintų visą frazę atbulai
Atskirtų žodžius ir juos atspausdintų
Žodį "Python" pakeistų į "Programming" ir atspausdintų naują sakinį
Patarimas: naudoti string karpymo įrankius, funkcijas split(), replace()

3 užduotis
Programoje išbandyti daugiau string funkcijų:

upper()
casefold()
capitalize()
count()
find()
ir t.t.
Visas jas galite rasti čia: https://www.w3schools.com/python/python_ref_string.asp

4 užduotis
Parašyti programą, kuri:

Leistų įvesti pirmą skaičių
Leistų įvesti antrą skaičių
Paklaustų, kokį matematinį veiksmą reiktų atliktų
Atspausdintų rezultatą: pasirinktų skaičių suma, daugybą ar pan.
Patarimas: naudoti input(), if, print

5 užduotis
Parašyti programą, kuri:

Leistų įvesti skaičių
Išvesti į ekraną „Skaičius yra lyginis“, jei taip yra
Išvesti į ekraną „Skaičius yra nelyginis“, jei taip yra
Išvesti į ekraną „Skaičius dalinasi iš 3“, jei skaičius dalinasi iš trijų
Patarimas: naudoti input(), if, print, %

The Zen of Python:

import this
