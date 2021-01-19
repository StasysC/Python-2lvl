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

## Kaip sukurti dekoratorių su parametrais:

```python
from time import sleep

def uzvelavimas(laikas):
    def uzvelavimas(fn):
        def wrapper(*args, **kwargs):
            sleep(laikas)
            print(f"Funkcija buvo atidėta {laikas} sekundę(-es)")
            return fn(*args, **kwargs)
        return wrapper
    return uzvelavimas

@uzvelavimas(1)
def for_sukimas(kartai):
    for x in range(kartai):
        print(x, " ", end="")
    print()

@uzvelavimas(3)
@args_counter
def sumavimas(*args):
    print("Skaičių suma:", sum(args))

for_sukimas(10000)

# Funkcija buvo atidėta 1 sekundę(-es)
# 0  1  2  3  4  5  6  7  8  9  10  11  12  13  14  15  16  17  18  19  20  21  22  23  24  25  26  27  28  29  30  31  32  33  34  35  36  37  38  39  40  41  42  43  44  45  46  47  48  49  50  51  52  53  54  55  56  57  58  59  60  61  62  63  64  65  66  67  68  69  70  71  72  73  74  75  76  77  78  79  80  81  82  83  84  85  86  87  88  89  90  91  92  93  94  95  96  97  98  99  
```
Dabar skirtingoms funkcijoms galime uždėti dekoratorių su skirtingais argumentais (šiuo atveju - funkcijos bus paleidžiamos su skirtingu užvėlavimu)

## Keli dekoratoriai ant funkcijos
Funkcijai galima uždėti ir kelis dekoratorius, pvz.:
```python
def uzvelavimas(laikas):
    def uzvelavimas(fn):
        def wrapper(*args, **kwargs):
            sleep(laikas)
            print(f"Funkcija buvo atidėta {laikas} sekundę(-es)")
            return fn(*args, **kwargs)
        return wrapper
    return uzvelavimas

def args_counter(fn):
    def wrapper(*args, **kwargs):
        print("Args number:", len(args))
        return fn(*args, **kwargs)
    return wrapper

@uzvelavimas(3)
@args_counter
def sumavimas(*args):
    print("Skaičių suma:", sum(args))

sumavimas(50, 30, 20, 15)

# Funkcija buvo atidėta 3 sekundę(-es)
# Args number: 4
# Skaičių suma: 115
```