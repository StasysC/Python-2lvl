## 1 užduotis
1. Pasiimti anksčiau sukurtą programos kodą
2. Funkcijas perdaryti taip, kad jos gražintų duomenis
3. Sukurti UNIT testą visoms funkcijoms
4. Kiekvienai funkcijai turi būti mažiausiai 3 patikrinimai
5. Maksimaliai patobulinti kodą, nuolatos leidžiant sukurtą UNIT testą
## 2 užduotis
1. Pasiimti anksčiau sukurtą programos kodą
2. Teste sukurti setUp() metodą, kuriame būtų inicijuotas klasės objektas
3. Funkcijas perdaryti taip, kad jos gražintų duomenis
4. Sukurti UNIT testą visoms funkcijoms
5. Kiekvienai funkcijai turi būti mažiausiai 3 patikrinimai
6. Maksimaliai patobulinti kodą, nuolatos leidžiant sukurtą UNIT testą
## 3 užduotis
Nuosekliai, papunkčiui, pagal duotą UNIT testą sukurti programą, skaičiuojančią KMI:
```python
import unittest
from kmi_skaiciavimas import kmi
class TestSkaiciavimas(unittest.TestCase):
    def test_kmi(self):
        self.assertEqual(23.54788069073783, kmi(78, 1.82))
        self.assertEqual(20.5456936226167, kmi(50, 1.56))
        self.assertEqual(27.70083102493075, kmi(100, 1.90))
        with self.assertRaises(ValueError):
            kmi(20, 1.40)
        with self.assertRaises(ValueError):
            kmi(240, 1.40)
        with self.assertRaises(ValueError):
            kmi(80, 0.40)
        with self.assertRaises(ValueError):
            kmi(80, 3.40)
```
