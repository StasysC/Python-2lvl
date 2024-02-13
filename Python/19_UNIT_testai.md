## Kaip patikrinti, ar programa teisingai veikia?
Failas: keliamieji.py:
```python
def ar_keliamieji(metai):
    if (metai % 400 == 0) or (metai % 100 != 0 and metai % 4 == 0):
        return("Keliamieji")
    else:
        return("Nekeliamieji")

print(ar_keliamieji(2000))
print(ar_keliamieji(2020))
print(ar_keliamieji(2100))

# Keliamieji
# Keliamieji
# Nekeliamieji
```
## Kaip ištestuoti programą UNIT testų pagalba
Failas: test_keliamieji.py:
```python
import unittest
from keliamieji import *

class TestKeliamieji(unittest.TestCase):

    def test_ar_keliamieji(self):
        rezultatas = ar_keliamieji(2000)
        lukestis = "Keliamieji"
        self.assertEqual(lukestis, rezultatas)

# Ran 1 test in 0.007s
# OK
```
## Testo paleidimas komandinėje eilutėje (cmd):
```
python -m unittest test_keliamieji.py

.
----------------------------------------------------------------------
Ran 1 test in 0.000s

OK
```
## Testo paleidimas tiesiogiai:
Faile test_keliamieji.py prirašyti:
```
if __name__ == '__main__':
    unittest.main()
```
Komandinėje eilutėje:
```
python test_keliamieji.py
```
**Pastaba:** paleidžiant testą PyCharm programoje, to nereikia

## Pats testas turi būti teisingas:
Failas: test_keliamieji.py:
```python
import unittest
from keliamieji import ar_keliamieji
class TestKeliamieji(unittest.TestCase):
    def test_ar_keliamieji(self):
        self.assertEqual("Keliamieji", ar_keliamieji(2000))
        self.assertEqual("Keliamieji", ar_keliamieji(2020))
        self.assertEqual("Keliamieji", ar_keliamieji(2100))


# Ran 1 test in 0.003s

# FAILED (failures=1)


# Nekeliamieji != Keliamieji

# Expected :Keliamieji
# Actual   :Nekeliamieji
```
Pataisome:
```python
import unittest
from keliamieji import ar_keliamieji
class TestKeliamieji(unittest.TestCase):
    def test_ar_keliamieji(self):
        self.assertEqual("Keliamieji", ar_keliamieji(2000))
        self.assertEqual("Keliamieji", ar_keliamieji(2020))
        self.assertEqual("Nekeliamieji", ar_keliamieji(2100))


# Ran 1 test in 0.002s

# OK
```
UNIT testų metodai:
[](https://github.com/StasysC/Python-2lvl/blob/master/Python/UNIT%20test%C5%B3%20metodai.png)

## Kai yra klaida kode:
Failas: keliamieji.py
```python
def ar_keliamieji(metai):
    if (metai % 400 == 0) or (metai % 4 == 0):
        return("Keliamieji")
    else:
        return("Nekeliamieji")
```
Leidžiant testą:
```
Ran 1 test in 0.003s

FAILED (failures=1)

Keliamieji != Nekeliamieji

Expected :Nekeliamieji
Actual   :Keliamieji
```
## Kita situacija:
Failas: aritmetika.py:
```python
def sudetis(a, b):
    return a + b

def atimtis(a, b):
    return a - b

def daugyba(a, b):
    return a * b

def dalyba(a, b):
    return a / b
```
Failas: test_aritmetika.py:
```python
import unittest
import aritmetika


class TestAritmetika(unittest.TestCase):
    def test_sudetis(self):
        self.assertEqual(15, aritmetika.sudetis(10, 5))
        self.assertEqual(0, aritmetika.sudetis(-1, 1))
        self.assertEqual(-2, aritmetika.sudetis(-1, -1))

    def test_atimtis(self):
        self.assertEqual(5, aritmetika.atimtis(10, 5))
        self.assertEqual(-2, aritmetika.atimtis(-1, 1))
        self.assertEqual(0, aritmetika.atimtis(-1, -1))

    def test_daugyba(self):
        self.assertEqual(50, aritmetika.daugyba(10, 5))
        self.assertEqual(-1, aritmetika.daugyba(-1, 1))
        self.assertEqual(1, aritmetika.daugyba(-1, -1))

    def test_dalyba(self):
        self.assertEqual(2, aritmetika.dalyba(10, 5))
        self.assertEqual(-1, aritmetika.dalyba(-1, 1))
        self.assertEqual(1, aritmetika.dalyba(-1, -1))


# Ran 4 tests in 0.002s

# OK
```
## Klaida daugyboje:
Failas: aritmetika.py:
```python
def sudetis(a, b):
    return a + b

def atimtis(a, b):
    return a - b

def daugyba(a, b):
    return a ** b

def dalyba(a, b):
    return a / b
```
Leidžiant testą:
```
Ran 4 tests in 0.004s

FAILED (failures=1)


100000 != 50

Expected :50
Actual   :100000
```
## Bet: kita klaida (dalyboje):
Failas: aritmetika.py:
```python
def sudetis(a, b):
    return a + b

def atimtis(a, b):
    return a - b

def daugyba(a, b):
    return a * b

def dalyba(a, b):
    return a // b
Leidžiant testą:

Ran 4 tests in 0.002s

OK
```
**Problema:** klaida kode yra, o testas jos nerodo

## Todėl taisome testą:
Faile test_aritmetika.py:
```python
def test_dalyba(self):
    self.assertEqual(2, aritmetika.dalyba(10, 5))
    self.assertEqual(-1, aritmetika.dalyba(-1, 1))
    self.assertEqual(1, aritmetika.dalyba(-1, -1))
    self.assertEqual(2.5, aritmetika.dalyba(5, 2))
```
Dabar leidžiant testą:
```
2 != 2.5

Expected :2.5
Actual   :2
```
Pataisome kodą

## Kaip patikrinti, ar kodas išmeta reikiamą klaidą
Faile test_aritmetika.py:
```python
def test_dalyba(self):
    self.assertEqual(2, aritmetika.dalyba(10, 5))
    self.assertEqual(-1, aritmetika.dalyba(-1, 1))
    self.assertEqual(1, aritmetika.dalyba(-1, -1))
    self.assertEqual(2.5, aritmetika.dalyba(5, 2))
    self.assertRaises(ZeroDivisionError, aritmetika.dalyba, 10, 0)
```
Leidžiant testą:
```
Ran 4 tests in 0.002s

OK
```
Arba:
```python
def test_dalyba(self):
    self.assertEqual(2, aritmetika.dalyba(10, 5))
    self.assertEqual(-1, aritmetika.dalyba(-1, 1))
    self.assertEqual(1, aritmetika.dalyba(-1, -1))
    self.assertEqual(2.5, aritmetika.dalyba(5, 2))
    with self.assertRaises(ZeroDivisionError):
        aritmetika.dalyba(10, 0)
```
## Kaip ištestuoti gražinamas True/False reikšmes:
Failas: keliamieji2.py:
```python
def ar_keliamieji2(metai):
    return (metai % 400 == 0) or (metai % 100 !=0 and metai % 4 == 0)
```
Failas: test_keliamieji2.py:
```python
import unittest
from keliamieji2 import ar_keliamieji2

class TestKeliamieji2(unittest.TestCase):
    def test_ar_keliamieji(self):
        self.assertTrue(ar_keliamieji2(2000))
        self.assertTrue(ar_keliamieji2(2020))
        self.assertFalse(ar_keliamieji2(2100))

# Ran 1 test in 0.002s

# OK
```
## Objektų klasių testavimas
Failas: keliamieji3.py:
```python
class Keliamieji:

    def tikrinti(self, metai):
        return (metai % 400 == 0) or (metai % 100 != 0 and metai % 4 == 0)

    def diapazonas(self, nuo, iki):
        sarasas = []
        for metai in range(nuo, iki):
            if (metai % 400 == 0) or (metai %100 != 0 and metai % 4 == 0):
                sarasas.append(metai)
        return sarasas
```
Failas: test_keliamieji3.py:
```python
import unittest
from keliamieji3 import Keliamieji

class TestKeliamieji3(unittest.TestCase):
    def test_tikrinti(self):
        objektas = Keliamieji()
        self.assertTrue(objektas.tikrinti(2000))
        self.assertTrue(objektas.tikrinti(2020))
        self.assertFalse(objektas.tikrinti(2100))

    def test_diapazonas(self):
        objektas = Keliamieji()
        rezultatas = objektas.diapazonas(1980, 2000)
        lukestis = [1980, 1984, 1988, 1992, 1996]
        self.assertEqual(lukestis, rezultatas)
```
## Patogesnis būdas:
Failas: test_keliamieji3.py
```python
import unittest
from keliamieji3 import Keliamieji

class TestKeliamieji3(unittest.TestCase):
    def setUp(self):
        self.objektas = Keliamieji()

    def test_tikrinti(self):
        self.assertTrue(self.objektas.tikrinti(2000))
        self.assertTrue(self.objektas.tikrinti(2020))
        self.assertFalse(self.objektas.tikrinti(2100))

    def test_diapazonas(self):
        rezultatas = self.objektas.diapazonas(1980, 2000)
        lukestis = [1980, 1984, 1988, 1992, 1996]
        self.assertEqual(lukestis, rezultatas)
```
## UNIT testų privalumai
* Galimybė išvengti klaidų rašant ar taisant kodą
* UNIT testai gali būti panaudoti kaip būsimos programos dokumentacija
* Sutaupo laiko testuotojų komandai
* Taupo pinigus (klaidų taisymas vėliau yra brangus)

## Testavimu paremtas programavimas (TDD)
Iš pradžių sukuriame testą – po to parašome kodą

# Užduotys
## 1 užduotis
Pasiimti anksčiau sukurtą programos kodą (4 paskaita "Funkcijos):
* Funkcijas perdaryti taip, kad jos gražintų duomenis
* Sukurti UNIT testą visoms funkcijoms
* Kiekvienai funkcijai turi būti mažiausiai 3 patikrinimai
* Maksimaliai patobulinti kodą, nuolatos leidžiant sukurtą UNIT testą
## 2 užduotis
Pasiimti anksčiau sukurtą programos kodą (4 paskaita "Funkcijos) sukurti klasę ir tada:
* Teste sukurti setUp() metodą, kuriame būtų inicijuotas klasės objektas
* Funkcijas perdaryti taip, kad jos gražintų duomenis
* Sukurti UNIT testą visoms funkcijoms
* Kiekvienai funkcijai turi būti mažiausiai 3 patikrinimai
* Maksimaliai patobulinti kodą, nuolatos leidžiant sukurtą UNIT testą
## 3 užduotis
Nuosekliai, papunkčiui, pagal duotą UNIT testą sukurti programą, skaičiuojančią KMI:
```python
import unittest
from kmi_skaiciavimas import kmi


class TestSkaiciavimas(unittest.TestCase):
    def test_kmi(self):
        self.assertEqual(23.5, kmi(78, 1.82))
        self.assertEqual(20.5, kmi(50, 1.56))
        self.assertEqual(27.7, kmi(100, 1.90))
        with self.assertRaises(ValueError):
            kmi(20, 1.40)
        with self.assertRaises(ValueError):
            kmi(240, 1.40)
        with self.assertRaises(ValueError):
            kmi(80, 0.40)
        with self.assertRaises(ValueError):
            kmi(80, 3.40)
```
