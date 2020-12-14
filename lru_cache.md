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
Pirmą kartą programa galvoja, tačiau antrą kartą skaičiavimo rezultatą traukia iš atminties. Dekoratoriaus parametruose galima nurodyti, kiek saugoti paskutinių reikšmių, numatytoji yra 128(?). 

```bash
python -i .\cache_pvz.py
labai galvoju
100000
100000
100000
>>> skaiciavimas(20, 20)
100000
>>> skaiciavimas(20, 30) 
labai galvoju
150000
>>> skaiciavimas(20, 30)
150000
>>> skaiciavimas(20, 30)
150000
>>> skaiciavimas(20, 40)
labai galvoju
200000
>>> skaiciavimas(20, 40)
200000
>>>
```