Functools modulyje guli nesudėtingas cach'inimo įrankis, kuris veikia taip:

```python
from functools import lru_cache
from time import sleep

@lru_cache()
def skaiciavimas(x, y):
    res = 250 * x * y
    print('labai galvoju')
    sleep(2)
    return res

print(skaiciavimas(20, 20))
print(skaiciavimas(20, 20))
print(skaiciavimas(20, 20))
```
rezultatas:
```bash
labai galvoju
100000
100000
100000
```
Pirmą kartą programa galvoja, tačiau antrą kartą skaičiavimo rezultatą traukia iš atminties. Dekoratoriaus parametruose galima nurodyti, kiek saugoti parametrų kombinacijų, numatytoji yra 128(?). Žemiau pavyzdys, kaip elgiasi funkcija, kuomet apribojame įsimenamų kombinacijų skaičių iki 3:

```bash
jt@jt-MS-7A34:~/Desktop/throw_aways$ python3 -i lru.py 
labai galvoju
100000
100000
100000
>>> skaiciavimas(10, 30)
labai galvoju
75000
>>> skaiciavimas(10, 30)
75000
>>> skaiciavimas(20, 30)
labai galvoju
150000
>>> skaiciavimas(20, 30)
150000
>>> skaiciavimas(30, 30)
labai galvoju
225000
>>> skaiciavimas(30, 30)
225000
>>> skaiciavimas(40, 30) # šis skaičiavimas iš cahe'o išstumia mūsų pirmąjį variantą
labai galvoju
300000
>>> skaiciavimas(40, 30)
300000
>>> skaiciavimas(10, 30) # pirmoji kombinacija, turi galvoti iš naujo.
labai galvoju
75000
>>> 
``` 