# Dekoratoriai
Dekoratoriai priima funkcijas, prie tų funkcijų prideda papildomą funkcionalumą, ir grąžina rezultatą. Dekoratorius yra šiek tiek sudėtinga perprasti, ir galbūt praktikoje patiems niekada neprireiks rašyti savo dekoratoriaus. Tačiau jų veikimo principą suprasti reikia todėl, kad su jais nuolat susidursime įvairiuose Python framework'uose. Tam, kad lengviau suprasti dekoratorius, pravartu susipažinti su higher order functions (aukštesnio rango funkcijos?)

Primityvus pavyzdys:

Turime funkciją, kuri grąžina tekstą:
```python
def returns_string(some_string):
    return some_string
```
Taip pat naudojame f-ją, kuri į parametrus priima kažkokį tekstą ir šalia jo funkciją:
```python
def returns_upper_string(text, func):
    if type(text) != str:
        return 'input must be a type of string'
    some_text = func(text)
    return some_text.upper()
```
f-ja patikrina, ar gautas parametras yra string tipo ir grąžina rezultatą visomis didžiosiomis raidėmis.
```python
print(returns_upper_string('higher order functions!', returns_string))

HIGHER ORDER FUNCTIONS!
```
Tai yra vadinamoji higher order function, jai kaip antras parametras tinka bet kokia funkcija, kuri grąžina tekstą. Pvz.:
```python
def returns_reversed_string(string):
    return string[::-1]

print(returns_upper_string('higher order functions!', returns_reversed_string))

#!SNOITCNUF REDRO REHGIH
```
Šiuo atveju sukūrėme dar vieną funkciją, kuri veikia analogiškai pirmąjai, tik tekstą grąžina atvirkščiai. Pasiūlius ją aukštesnio rango funkcijai, ji ją puikiai priėmė, bei nuo savęs pridėjo papildomo funkcionalumo - ALL CAPS :)

Dabar pamėginsime analogišką rezultatą išgauti rašant dekoratorių:
```python
def upper_decorator(func):
    def wrapper(our_text):
        if type(our_text) != str:
            return 'input must be a type of string'
        some_text = func(our_text)
        return some_text.upper()
    return wrapper
```
Kaip matome, dekoratorius rašomas labai panašiai, kaip ir mūsų aukštesnio rango funkcija, tik jos turinys "suvyniojamas" į apvalkalą (wrapper). Į dekoratoriaus parametrus dedame funkciją, kurią jis "apgaubs". Wrapper parametruose - tos funkcijos parametrai.

Parašius dekoratorių, python mums leidžia "apvilkti" savo funkcijas naudojant tokią sintaksę:
```python
@upper_decorator
def returns_string(some_string):
    return some_string

@upper_decorator
def returns_reversed_string(string):
    return string[::-1]
```
ir paskui ją labai paprastai iškviesti:
```python
print(returns_string('Decorator!'))
print(returns_reversed_string('Decorator!'))

# DECORATOR!
# !ROTAROCED
```
Praktikoje savo dekoratorių rašymas menkai tikėtinas, tačiau jie labai paplitę pvz. backend'o framework'uose, tokiuose, kaip Django arba Flask. Pvz.:
```python
from flask import Flask
app = Flask(__name__)

@app.route('/')
def hello_world():
    return 'Hello, World!'
```
Šiuo atveju nepasimesime ir suprasime, kad mūsų funkciją hello_world gaubia Flask'o modulyje įrašytas dekoratorius route.

## Dekoratoriai su argumentais
Prieš tai nagrinėtas dekoratorius (grąžinantis ALL CAPS) turėjo trūkumą - jis priėmė funkcijas tik su fiksuotu kiekiu argumentų(1). Galima rašyti lankstesnius dekoratorius. Tarkime, turime funkcijas, grąžinančias integer reikšmes:
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
```python
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

## Dekoratorių meta info
Dekoratorių elgsenoje nėra numatytas funkcijos metaduomenų išsaugojimas. Metaduomenų Python'as ieško ne funkcijoje, kurią iškviečiame, o pačiame warapper'yje. Pvz, jeigu modifikuotumėm mūsų dekoratorių tokiu būdu:
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
problema sprendžiasi paprastai. Iš functools reikia imporrtuoti wraps ir panaudoti taip:
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
kaip matome, wraps yra ne kas kita, o dekoratorius :) šį kartą spausdindami funkcijos metaduomenis, gausime, ko tikėjomės:
```python
print(give_me_10.__name__)
print(give_me_10.__doc__)

# give_me_10
# Grąžina skaičių 10
```
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
Dabar ant funkcijos sumavimas uždėjome du dekoratorius – uzvelavimas (jis užvėlina programos paleidimą 3 sekundėmis) ir args_counter (jis suskaičiuoja funkcijai paduotus argumentus). Paleidus šią funkciją, ji pereina ir per abu dekoratorius ir padaro atitinkamą veiksmą.

# Užduotys
## 1 Užduotis
Parašykite dekoratorių kuris riboja parametrų kiekį (tarkime, ne daugiau negu 2 parametrai funkcijai)

## 2 Užduotis
Parašykite dekoratorių, kuris atideda funkcijos vykdymą 3s

## 3 Užduotis
Parašykite dekoratorių, kuris leidžia į funkciją įrašyti tik string tipo parametrus ir turi galimybę būti panaudotas kaip papildomas dekoratorius.

## 4 Užduotis
Turime tokį kodą:
```python
import requests  # importuojame requests
from time import time  # importuojame time modulį

start_time = time()  # fiksuojame starto laiką
r = requests.get('http://www.cnn.com')  # sukuriame http užklausą
print(r.status_code)  # spausdiname status code (200 = OK, 404 = Not Found, ir t.t. galima pasiguglinti http status codes)
end_time = time()  # fiksuojame pabaigos laiką
print(end_time - start_time)  # atspausdiname laiką, per kurį gaovme atsakymą
```
Parašykite dekoratorių, bet kokios funkcijos vykdymo laikui fiksuoti. Galite patobulinti, pvz funkcijos (vardas), su tokiais ir tokiais argumentais vykdymo laikas - XX s. Ištestuokite, su funkcija, grąžinančia svetainės atsako kodą ir su funkcija, išrenkančia pirminius skaičius užduotame diapazone.
