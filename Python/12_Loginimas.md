## Kaip tikrinti kodą PRINT funkcijų pagalba:
```python
def dalyba(a, b):
    padalinom = a / b
    print(f"Dalyba: {a} / {b} = {padalinom}")
    return padalinom

dalyba(10, 5)

# Dalyba: 10 / 5 = 2.0
```
## Kaip tikrinti kodą loginimo pagalba:
```python
import logging

def dalyba(a, b):
    rezultatas = a / b
    logging.warning(f"Paleista funkcija {dalyba.__name__}, sudėti skaičiai {a} ir {b}, rezultatas = {rezultatas}")
    return rezultatas

padalinom = dalyba(10, 5)

# WARNING:root:Paleista funkcija dalyba, sudėti skaičiai 10 ir 5, rezultatas = 2.0
```
Bet: taip negerai, nes informacija apie atliktus veiksmus neturi būti warning lygio

## Kokie yra loginimo pranešimų lygiai:
**DEBUG** Detailed information, typically of interest only when diagnosing problems.

**INFO** Confirmation that things are working as expected.

**WARNING** An indication that something unexpected happened, or indicative of some problem in the near future (e.g. ‘disk space low’). The software is still working as expected.

**ERROR** Due to a more serious problem, the software has not been able to perform some function.

**CRITICAL** A serious error, indicating that the program itself may be unable to continue running.

## Kaip nustatyti loginimo pranešimų lygį:
```python

import logging

logging.basicConfig(level=logging.DEBUG)

def dalyba(a, b):
    rezultatas = a / b
    logging.info(f"Paleista funkcija {dalyba.__name__}, sudėti skaičiai {a} ir {b}, rezultatas = {rezultatas}")
    return rezultatas

dalyba(10, 5)

# INFO:root:Paleista funkcija dalyba, sudėti skaičiai 10 ir 5, rezultatas = 2.0
```
## Kaip nustatyti loginimą į failą:
```python
import logging

logging.basicConfig(filename="aritmetika.log", encoding="UTF-8", level=logging.DEBUG)

def dalyba(a, b):
    rezultatas = a / b
    logging.info(f"Paleista funkcija {dalyba.__name__}, skaičius {a} padalintas iš {b}, rezultatas = {rezultatas}")
    return rezultatas

dalyba(10, 5)
```
**faile aritmetika.log:**
```python
# INFO:root:Paleista funkcija dalyba, sudėti skaičiai 10 ir 5, rezultatas = 2.0
```
## Kaip nustatyti loginimo pranešimų formatą:
https://docs.python.org/3/library/logging.html#logrecord-attributes
```python
import logging

logging.basicConfig(filename='aritmetika.log', encoding="UTF-8",
level=logging.DEBUG, format='%(asctime)s:%(levelname)s:%(name)s:%(message)s')

def dalyba(a, b):
    rezultatas = a / b
    logging.info(f"Paleista funkcija {dalyba.__name__}, sudėti skaičiai {a} ir {b}, rezultatas = {rezultatas}")
    return rezultatas

dalyba(10, 5)
```
**faile aritmetika.log:**
```python
2022-09-14 11:31:20,949:INFO:Paleista funkcija dalyba, sudėti skaičiai 10 ir 5, rezultatas = 2.0
```
## Loginimas su objektais:
```python
import logging

logging.basicConfig(filename='asmenys.log', encoding="UTF-8",
level=logging.INFO, format='%(asctime)s:%(levelname)s:%(message)s')

class Asmuo:

    def __init__(self, vardas, pavarde):
        self.vardas = vardas
        self.pavarde = pavarde
        logging.info(f"Sukurtas darbuotojas: {self.vardas} {self.pavarde}")

tadas = Asmuo("Tomas", "Kucinskas")
rokas = Asmuo("Rokas", "Radzevicius")
```
**faile asmenys.log:**
```python
2020-04-13 15:31:00,451:INFO:Sukurtas darbuotojas: Tomas Kucinskas
2020-04-13 15:31:00,451:INFO:Sukurtas darbuotojas: Rokas Radzevicius
```
## Savo logerio sukūrimas:
**Faile asmenys.py:**
```python
import logging

logging.basicConfig(filename='asmenys.log', encoding="UTF-8",
level=logging.INFO, format='%(asctime)s:%(levelname)s:%(message)s')

class Asmuo:

    def __init__(self, vardas, pavarde):
        self.vardas = vardas
        self.pavarde = pavarde
        logging.info(f"Sukurtas darbuotojas: {self.vardas} {self.pavarde}")

tadas = Asmuo("Tomas", "Kucinskas")
rokas = Asmuo("Rokas", "Radzevicius")
```
**Faile aritmetika.py:**
```python
import logging
import asmenys

logging.basicConfig(filename='aritmetika.log', encoding="UTF-8",
level=logging.DEBUG, format='%(asctime)s:%(levelname)s:%(name)s:%(message)s')


def dalyba(a, b):
    rezultatas = a / b
    logging.info(f"Paleista funkcija {dalyba.__name__}, sudėti skaičiai {a} ir {b}, rezultatas = {rezultatas}")
    return rezultatas

dalyba(10, 5)
```
Rezultatas:
Failo aritmetika.log nėra!
**Faile asmenys.log:**
```python
2022-09-14 11:52:07,001:INFO:Sukurtas darbuotojas: Tomas Kucinskas
2022-09-14 11:52:07,001:INFO:Sukurtas darbuotojas: Rokas Radzevicius
2022-09-14 11:52:07,001:INFO:Paleista funkcija dalyba, sudėti skaičiai 10 ir 5, rezultatas = 2.0
```
Problema!

Sprendimas:

**Faile aritmetika.py:**
```python
import logging
logger = logging.getLogger(__name__)
file_handler = logging.FileHandler('aritmetika.log')
logger.addHandler(file_handler)

logger.setLevel(logging.DEBUG)

formatter = logging.Formatter('%(asctime)s:%(levelname)s:%(name)s:%(message)s')
file_handler.setFormatter(formatter)

def dalyba(a, b):
    rezultatas = a / b
    logger.info(f"Paleista funkcija {dalyba.__name__}, sudėti skaičiai {a} ir {b}, rezultatas = {rezultatas}")
    return rezultatas

dalyba(10, 5)
```
**Faile aritmetika.log:**
```python
2022-09-14 11:52:07,001:INFO:Paleista funkcija dalyba, sudėti skaičiai 10 ir 5, rezultatas = 2.0
```
Tą patį galime padaryti ir faile asmenys.py:
```python
import logging

logger = logging.getLogger(__name__)
file_handler = logging.FileHandler('asmenys.log')
logger.addHandler(file_handler)
logger.setLevel(logging.DEBUG)
formatter = logging.Formatter('%(asctime)s:%(levelname)s:%(name)s:%(message)s')
file_handler.setFormatter(formatter)

class Asmuo:

    def __init__(self, vardas, pavarde):
        self.vardas = vardas
        self.pavarde = pavarde
        logger.info(f"Sukurtas darbuotojas: {self.vardas} {self.pavarde}")

tadas = Asmuo("Tomas", "Kucinskas")
rokas = Asmuo("Rokas", "Radzevicius")
```
## Kaip loginti ir į failą ir į konsolę:
```python
import logging
logger = logging.getLogger(__name__)
file_handler = logging.FileHandler('aritmetika.log')
logger.addHandler(file_handler)

logger.setLevel(logging.DEBUG)

formatter = logging.Formatter('%(asctime)s:%(levelname)s:%(name)s:%(message)s')
file_handler.setFormatter(formatter)

stream_handler = logging.StreamHandler()
stream_handler.setFormatter(formatter)
logger.addHandler(stream_handler)

def dalyba(a, b):
    rezultatas = a / b
    logger.info(f"Paleista funkcija {dalyba.__name__}, sudėti skaičiai {a} ir {b}, rezultatas = {rezultatas}")
    return rezultatas

dalyba(10, 5)
```
**Ir faile aritmetika.log ir konsolėje**

## Kaip loginti klaidas:
```python
import logging
logger = logging.getLogger(__name__)
file_handler = logging.FileHandler('aritmetika.log')
logger.addHandler(file_handler)

logger.setLevel(logging.DEBUG)

formatter = logging.Formatter('%(asctime)s:%(levelname)s:%(name)s:%(message)s')
file_handler.setFormatter(formatter)

stream_handler = logging.StreamHandler()
stream_handler.setFormatter(formatter)
logger.addHandler(stream_handler)

def dalyba(a, b):
    try:
        rezultatas = a / b

    except ZeroDivisionError:
        logger.exception("Dalyba is nulio")
    else:
        return rezultatas

a = 20
b = 0

padalinom = dalyba(a, b)
logger.info(f"Dalyba: {a} / {b} = {padalinom}")
```
**Ir faile aritmetika.log ir konsolėje:**
```python
2020-04-13 15:53:35,486:ERROR:__main__:Dalyba is nulio
Traceback (most recent call last):
  File "C:/Users/Donoras/PycharmProjects/loginimas_12/aritmetika.py", line 17, in dalyba
    rezultatas = a / b
ZeroDivisionError: division by zero
```
# Užduotys:
## 1 užduotis
Sukurti funkcijas, kurios:

* Gražintų visų paduotų skaičių sumą (su *args argumentu)
* Gražintų paduoto skaičiaus šaknį (panaudoti math.sqrt())
* Gražintų paduoto sakinio simbolių kiekį (su len())
* Gražintų rezultatą, skaičių x padalinus iš y

Nustatyti standartinį logerį (logging) taip, kad jis:

* Saugotų pranešimus į norimą failą
* Saugotų INFO lygio žinutes
* Pranešimai turi būti tokiu formatu: data/laikas, lygis, žinutė

Kiekviena funkcija turi sukurti INFO lygio log pranešimą apie tai, ką atliko, pvz.:
```python
logging.info(f"Skaiciu {args} suma lygi: {sum(args)}")
```
Paleisti kiekvieną funkciją su norimais argumentais

## 2 užduotis
Perdaryti 1 užduoties programą, kad:

* Į šaknies funkciją padavus string tipo argumetrą, į log failą būtų išsaugoma išimties klaida su norimu tekstu
* Į dalybos funkciją antrą argumentą padavus 0, į log failą būtų išsaugoma išimties klaida su norimu tekstu
**Patarimas:** panaudoti try/except/else, logging.exception()

## 3 užduotis
Perdaryti 2 užduoties programą, kad:

* Būtų sukurtas savo logeris, kuris fiksuotų visus anksčiau aprašytus pranešimus
* Sukurtas logeris ne tik išsaugotų pranešimus faile, bet ir atvaizduotų juos konsolėje
