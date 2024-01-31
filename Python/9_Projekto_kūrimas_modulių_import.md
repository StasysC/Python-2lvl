# Kaip sukurti projektą su daug katalogų ir failų
### Projekte turime du .py failus

Failas mano_modulis.py:
```python
kintamasis = "Čia yra testinis kintamasis"

print("mano_modulis sėkmingai importuotas!")

def parasyti_atbulai(sakinys):
    print(sakinys[::-1])

```
Failas mano_pagrindinis.py:

```python
import mano_modulis

sakinys = "Sveikas, pasauli!"
atbulai = mano_modulis.parasyti_atbulai(sakinys)

# mano_modulis sėkmingai importuotas!
# !iluasap ,sakievS

```
## Importuoti modulį kaip:

```python
import mano_modulis as mm

sakinys = "Sveikas, pasauli!"
atbulai = mm.parasyti_atbulai(sakinys)

# mano_modulis sėkmingai importuotas!
# !iluasap ,sakievS

```
## Importuoti tik funkciją:

```python
from mano_modulis import parasyti_atbulai

sakinys = "Sveikas, pasauli!"
atbulai = parasyti_atbulai(sakinys)

# mano_modulis sėkmingai importuotas!
# !iluasap ,sakievS

```
Importuoti daugiau:

```python
from mano_modulis import parasyti_atbulai, kintamasis

sakinys = "Sveikas, pasauli!"
atbulai = parasyti_atbulai(sakinys)
print(kintamasis)

# mano_modulis sėkmingai importuotas!
# !iluasap ,sakievS
# Čia yra testinis kintamasis
```
## Importuoti vieną jų kaip trumpinį:

```
from mano_modulis import parasyti_atbulai as pa, kintamasis

sakinys = "Sveikas, pasauli!"
atbulai = pa(sakinys)
print(kintamasis)

# mano_modulis sėkmingai importuotas!
# !iluasap ,sakievS
# Čia yra testinis kintamasis

```
## Importuoti viską:
```python
from mano_modulis import *

sakinys = "Sveikas, pasauli!"
atbulai = parasyti_atbulai(sakinys)
print(kintamasis)

# mano_modulis sėkmingai importuotas!
# !iluasap ,sakievS
# Čia yra testinis kintamasis
```
## Kad kodas būtų paleidžiamas tik tiesiogiai paleidžiant failą:
```python
kintamasis = "Čia yra testinis kintamasis"

print("mano_modulis sėkmingai importuotas!")

def parasyti_atbulai(sakinys):
    print(sakinys[::-1])

if __name__ == '__main__':
    print("Kodas vykdomas tik leidžiant tiesiogiai")
```
Failas mano_pagrindinis.py:
```python
import mano_modulis

sakinys = "Sveikas, pasauli!"
atbulai = mano_modulis.parasyti_atbulai(sakinys)

# mano_modulis sėkmingai importuotas!
# !iluasap ,sakievS
```
# Importuoti modulį iš kito katalogo:
### Projekte turime du .py failus, taip pat katalogą moduliai su dar vienu .py failu

Failas moduliai/mano_modulis_3.py:
```python
kintamasis3 = "Čia yra testinis kintamasis 3"

print("mano_modulis_3 sėkmingai importuotas!")

def parasyti_atbulai3(sakinys):
    print(sakinys[::-1])
```
Failas mano_pagrindinis.py (neteisingas import):
```python
import mano_modulis_3

# ModuleNotFoundError: No module named 'mano_modulis_3'
```
Teisingas import:
```python
import moduliai.mano_modulis_3 as mm3
print(mm3.kintamasis3)

# mano_modulis_3 sėkmingai importuotas!
# Čia yra testinis kintamasis 3
```
## Kaip importuoti modulius iš to paties katalogo (absolute import):
Failas moduliai/mano_pagrindinis_3.py:
```python
from moduliai.mano_modulis_3 import kintamasis3

print(kintamasis3)

# mano_modulis_3 sėkmingai importuotas!
# Čia yra testinis kintamasis 3
```
## Kitas importavimo iš to paties katalogo būdas (relative import):
Failas moduliai/mano_pagrindinis_3.py:
```python
from .mano_modulis_3 import kintamasis3

print(kintamasis3)

# mano_modulis_3 sėkmingai importuotas!
# Čia yra testinis kintamasis 3
```
. – tame pačiame pakete (kataloge)

.. – aukščiau esančiame pakete (kataloge)


# Importavimas iš standartinės Python bibliotekos
```python
import random

pasirinkimai = ["Istorija", "Fizika", "Medicina", "Informatika"]
pasirinktas_kursas = random.choice(pasirinkimai)
print(pasirinktas_kursas)

# Istorija
```
```python
import math

saknis = math.sqrt(9)
print(saknis)

# 3
```
```python
from datetime import date
import calendar

print(date.today())
print(calendar.isleap(2017))
print(calendar.isleap(2020))

# 2019-03-29
# False
# True
```
```python
import os

print(os.getcwd())

# C:\Users\Donoras\CodeAcademy\projektas
```
## Visi standartinės Python bibliotekos moduliai:
https://docs.python.org/3/library/

# Užduotys
## 1 užduotis
Python faile padaryti šiuos veiksmus (atskirai, ne iškart):

* Importuoti modulį datetime. Atsispausdinti šiandienos datą ir laiką kartu, tik datą (date.today()) bei tik laiką (.now().time()).
* Iš paketo datetime importuoti modulį date. Atsispausdinti šiandienos datą.
* Iš paketo datetime importuoti modulį date kaip data (as data). Atsispausdinti šiandienos datą.

## 2 užduotis
Sukurti naują projektą (PyCharm programoje) Jame sukurti failą modulis.py, kuriame:

* Kintamajam kintamasis priskirti reikšmę „Čia yra kintamasis“
* Sukurti funkciją funkcija(), kuri atspausdina „Čia yra funkcija“.
* Sukurti klasę Objektas, kurį iniciavus atspausdina „Čia yra klasė“.

Sukurti failą main.py, kuriame:
* Importuoti modulį modulis
* Atspausdinti importuotą kintamąjį kintamasis
* Paleisti importuotą funkciją funkcija()
* Inicijuoti importuotos klasės Objektas() objektą

## 3 užduotis
* Sukurti naują projektą mokymas
* Projekto kataloge sukurti katalogą modules
* Kataloge modules sukurti failą kursas.py
* Faile kursas.py sukurti objekto klasę Kursas, kuri turėtų savybes pavadinimas, destytojas, trukme, taip pat metodą destyti(), kuris spausdintų „Vyksta mokymas!“
* Kataloge modules sukurti antrą failą python_kursas.py
* Faile python_kursas.py sukurti objekto klasę PythonKursas, kuri paveldėtų viską iš klasės Kursas, bei perrašytų metodą destyti() taip, kad jis spausdintų „Vyksta programavimas!“
* Pagrindiniame projekto kataloge sukurti failą main.py
* Faile main.py importuoti PythonKursas modulį (failą)
* Faile main.py inicijuoti Kursas objektą su norimomis savybėmis
* Faile main.py inicijuoti PythonKursas objektą su norimomis savybėmis
* Paleisti abiejų objektų metodą destyti()

## 4 užduotis
Perdaryti biudžeto programą su klasėmis (iš 6 paskaitos) taip, kad visos klasės būtų skirtinguose failuose.
