prieš tai nagrinėtas dekoratorius (grąžinantis ALL CAPS) turėjo trūkumą - 
jis priėmė funkcijas tik su fiksuotu kiekiu argumentų(1). Galima rašyti lankstesnius dekoratorius.
Tarkime, turime funkcijas, grąžinančias integer reikšmes:

```python
def give_me_10():
    return 10


def multiply(x, y):
    return x * y


def sum_all(*args):
    return sum(args)
``` 

Parašykime dekoratorių, kuris priima visas tris funkcijas:

```python
def lyginis_nelyginis(func):
    def wrapper(*args, **kwargs):
        result = func(*args, **kwargs)
        if (result % 2) != 0:
            return result, 'nelyginis!'
        return result, 'lyginis!'
    return wrapper
```

Įvilkime savo f-jas į dekoratorių:

```python
@lyginis_nelyginis
def give_me_10():
    return 10

@lyginis_nelyginis
def multiply(x, y):
    return x * y

@lyginis_nelyginis
def sum_all(*args):
    return sum(args)
```
atspausdinkime rezultatus:
```python
print(give_me_10())
print(multiply(5,5))
print(sum_all(10, 3, 7, 8))

# (10, 'lyginis!')
# (25, 'nelyginis!')
# (28, 'lyginis!')
```

Tai yra standartinis universalaus dekoratoriaus rašymo būdas.

Dekoratorių elgsenoje nėra numatytas funkcijos metaduomenų išsaugojimas. Metaduomenų Python'as 
ieško ne funkcijoje, kurią iškviečiame, o pačiame warapper'yje. Pvz, jeigu modifikuotumėm mūsų 
dekoratorių tokiu būdu:

```python
def lyginis_nelyginis(func):
    def wrapper(*args, **kwargs):
        """I'm a holly wrapper!!!"""
        result = func(*args, **kwargs)
        if (result % 2) != 0:
            return result, 'nelyginis!'
        return result, 'lyginis!'
    return wrapper
```

ir kurią nors iš f-jų dokumentuotumėm:

```python
@lyginis_nelyginis
def give_me_10():
    """Grąžina skaičių 10"""
    return 10
```

pabandę atsispausdinti metaduomenis, gautumėm:

```python
print(give_me_10.__name__)
print(give_me_10.__doc__)

# wrapper
# I'm a holly wrapper!!!
```

problema sprendžiasi paprastai. Iš *functools* reikia imporrtuoti *wraps* 
ir panaudoti taip:

```python
from functools import wraps

def lyginis_nelyginis(func):
    @wraps(func)
    def wrapper(*args, **kwargs):
        """I'm a holly wrapper!!!"""
        result = func(*args, **kwargs)
        if (result % 2) != 0:
            return result, 'nelyginis!'
        return result, 'lyginis!'
    return wrapper
```
kaip matome, wraps yra ne kas kita, o dekoratorius :)
šį kartą spausdindami funkcijos metaduomenis, gausime, ko tikėjomės:

```python
print(give_me_10.__name__)
print(give_me_10.__doc__)

# give_me_10
# Grąžina skaičių 10