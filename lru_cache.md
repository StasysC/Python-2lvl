Functools modulyje guli nesudėtingas cach'inimo įrankis, kuris veiia taip:

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

```bash
labai galvoju
100000
100000
100000
```