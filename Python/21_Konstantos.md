# Konstantos

Python neturi įprastų konstantų, todėl vietoje to tiesiog rašomas kintamasis didžiosiomis raidėmis. Turint omeny, kad tokio kintamojo reikšmės programos nereikėtų keisti:
```python
PI = 3.14
GRAVITACIJA = 9.8

print(PI)
     
# 3.14
```
Enum – tai konstantų rinkiniai, paprastai apibrėžiami atskirose klasėse, paveldinčiose Enum.

Pvz., šiame Enum apibrėžėme savaitės dienas:
```python
from enum import Enum

class Savaitė(Enum):
  PIRMADIENIS = 1
  ANTRADIENIS = 2
  TRECIADIENIS = 3
  KETVIRTADIENIS = 4
  PENKTADIENIS = 5
  SESTADIENIS = 6
  SEKMADIENIS = 7
     

print(Savaitė.PENKTADIENIS)
     
# Savaitė.PENKTADIENIS
```
```python
diena = Savaitė.SEKMADIENIS
print(diena)
print(diena.name)
print(diena.value)
     
# Savaitė.SEKMADIENIS
# SEKMADIENIS
# 7
```
## Kaip atspausdinti visas enum reikšmes:
```python
print(list(Savaitė))
     
# [<Savaitė.PIRMADIENIS: 1>, <Savaitė.ANTRADIENIS: 2>, <Savaitė.TRECIADIENIS: 3>, <Savaitė.KETVIRTADIENIS: 4>, <Savaitė.PENKTADIENIS: 5>, <Savaitė.SESTADIENIS: 6>, <Savaitė.SEKMADIENIS: 7>]
```
```python
for x in Savaitė:
    print(x.name, x.value)
   
# PIRMADIENIS 1
# ANTRADIENIS 2
# TRECIADIENIS 3
# KETVIRTADIENIS 4
# PENKTADIENIS 5
# SESTADIENIS 6
# SEKMADIENIS 7
```
```python
for key, value in Savaitė.__members__.items():
    print(key, value)
     
# PIRMADIENIS Savaitė.PIRMADIENIS
# ANTRADIENIS Savaitė.ANTRADIENIS
# TRECIADIENIS Savaitė.TRECIADIENIS
# KETVIRTADIENIS Savaitė.KETVIRTADIENIS
# PENKTADIENIS Savaitė.PENKTADIENIS
# SESTADIENIS Savaitė.SESTADIENIS
# SEKMADIENIS Savaitė.SEKMADIENIS
```
## Kaip sukurti enum su daugiau reikšmių:
```python
class Menuo(Enum):
    SAUSIS = "Sausis", 1
    VASARIS = "Vasaris", 2
    KOVAS = "Kovas", 3
    BALANDIS = "Balandis", 4
    GEGUZE = "Gegužė", 5
    BIRZELIS = "Birželis", 6
    LIEPA = "Liepa", 7
    RUGPJUTIS = "Rugpjūtis", 8
    RUGSEJIS = "Rugsėjis", 9
    SPALIS = "Spalis", 10
    LAPKRITIS = "Lapkritis", 11
    GRUODIS = "Gruodis", 12
     

print(Menuo.BIRZELIS)
     
# Menuo.BIRZELIS
```
```python
menuo = Menuo.GEGUZĖ
print(menuo.name)
print(menuo.value)
print(menuo.value[0])
print(menuo.value[1])
     
# GEGUZE
# ('Gegužė', 5)
# Gegužė
# 5
```
## Kaip sukurti enum su automatinėmis reikšmėmis:
```python
from enum import Enum, auto

class Spalva(Enum):
  JUODA = auto()
  BALTA = auto()
  RAUDONA = auto()
  ZALIA = auto()
  GELTONA = auto()
  MELYNA = auto()
     

spalva = Spalva.RAUDONA
print(spalva)
print(spalva.name)
print(spalva.value)
     
# Spalva.RAUDONA
# RAUDONA
# 3
```
## Kaip sukurti enum su unikaliomis reikšmėmis:
```python
from enum import Enum, auto, unique

class Neunikalus(Enum):
  VIENAS = 1
  DU = 2
  DARDU = 2

print(2)

# 2
```
```python
from enum import Enum, auto, unique

@unique
class Neunikalus(Enum):
  VIENAS = 1
  DU = 2
  DARDU = 2
     
# ValueError: duplicate values found in <enum 'Neunikalus'>: DARDU -> DU
```

## Enum panaudojimo įvedime pavyzdys:
```python
class Veiksmas(Enum):
  IVESTI = 1
  ATSPAUSDINTI = 2
  ISEITI = 3


def atlikti_veiksma(veiksmas: Veiksmas):
  print(f"Veiksmas įvykdytas: {veiksmas.name}")
  # print(f"Veiksmas {veiksmas.value{[0]}}")
  

# Įvedimas ir funkcijos kvietimas:
for veiksmas in Veiksmas:
  print(f"{veiksmas.value} - {veiksmas.name}")

ivesta = int(input("Pasirinkite veiksmą: "))
atlikti_veiksma(Veiksmas(ivesta))
     
# 1 - IVESTI
# 2 - ATSPAUSDINTI
# 3 - ISEITI
# Pasirinkite veiksmą: 2
# Veiksmas įvykdytas: ATSPAUSDINTI
```
# Užduotys
## 1 užduotis
Perdaryti biudžeto programą taip, kad vietoje įprastų pajamų ir išlaidų kintamųjų, būtų naudojami enum (jei nenorite gadinti jau veikiančios programos, pasidarykite kopiją, arba tiesiog naudokite github :)
