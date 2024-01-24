# Funkcijos
![](https://github.com/StasysC/Python-2lvl/blob/master/Python/funkcijos_schema.png)
```python
def pasisveikinti():
    print("Sveikas, pasauli!")

pasisveikinti()
pasisveikinti()
pasisveikinti()

# Sveikas, pasauli!
# Sveikas, pasauli!
# Sveikas, pasauli!
```
## Funkcijos su argumentais:
```python
def pasisveikinti(vardas):
    print(f"Sveikas, {vardas}")

pasisveikinti("Tomas")
pasisveikinti("Jonas")
pasisveikinti("")

# Sveikas, Tomas
# Sveikas, Jonas
# Sveikas,
```
```python
def kvadratas(skaicius):
    kvadratu = skaicius ** 2
    print(kvadratu)

kvadratas(2)
# 4
```
## Funkcijos su gražinama reikšme (return):
Funkcijos be return trūkumas:
```python
def kvadratu(skaicius):
    rezultatas = skaicius ** 2
    print(rezultatas)

kvadratu(3)
# 9

daugyba = kvadratu(3) * 2
print(daugyba)
# TypeError: unsupported operand type(s) for *: 'NoneType' and 'int'

print(kvadratu(3))
None
```
Su return:
```python
def kvadratu(skaicius):
    rezultatas = skaicius ** 2
    return rezultatas

daugyba = kvadratu(3) * 2
print(daugyba)
# 18
```
## Funkcijos su keliais argumentais:
```python
def skaiciu_suma(skaicius1, skaicius2, skaicius3):
    suma = skaicius1 + skaicius2
    daugyba = suma * skaicius3
    return daugyba

print(skaiciu_suma(2, 5, 20))
# 140
```
## Funkcijos su nebūtinais argumentais:
```python
def skaiciu_suma(skaicius1, skaicius2, skaicius3=1):
    rezultatas = (skaicius1 + skaicius2) * skaicius3
    return rezultatas


print(skaiciu_suma(2, 5, 4))
# 28

print(skaiciu_suma(2, 5))
# 7
```
```python
def skaiciu_suma(skaicius1=10, skaicius2=10, skaicius3=1):
    rezultatas = (skaicius1 + skaicius2) * skaicius3
    return rezultatas

print(skaiciu_suma())
print(skaiciu_suma(2))
print(skaiciu_suma(2, 5))
print(skaiciu_suma(2, 5, 4))

# 20
# 12
# 7
# 28
```
## Kaip priskirti konkretų argumentą (-us):
```python
def skaiciu_suma(skaicius1=10, skaicius2=10, skaicius3=1):
    rezultatas = (skaicius1 + skaicius2) * skaicius3
    return rezultatas

print(skaiciu_suma(skaicius3=3))
print(skaiciu_suma(skaicius1=20, skaicius3=3))

# 60
# 90
```
## Funkcijos su neribotais argumentais:
```python
def daug_kvadratu(*args):
    for skaicius in args:
        print(skaicius ** 2)

daug_kvadratu(4, 5, 7, 8, 9, 10)

# 16
# 25
# 49
# 64
# 81
# 100
```
```python
def spausdinti_reiksmes(**kwargs):
    for raktas, reiksme in kwargs.items():
        print(raktas, reiksme)

spausdinti_reiksmes(vardas="Tomas", pavarde="Rutkauskas", lytis="Vyras", amzius=29, daiktai=["Telefonas", "Ausinės", "Krepšys"])

# vardas Tomas
# pavarde Rutkauskas
# lytis Vyras
# amzius 29
# daiktai ['Telefonas', 'Ausinės', 'Krepšys']
```
## Funkcijos su įprastais ir neribotais argumentais:
```python
def spausdinti_reiksmes(vardas, pavarde, **kwargs):
    print(f"Vardas: {vardas}, Pavardė: {pavarde}")
    for raktas, reiksme in kwargs.items():
        print(raktas, reiksme)

spausdinti_reiksmes("Tomas", "Rutkauskas", lytis="Vyras", amzius=29, daiktai=["Telefonas", "Ausinės", "Krepšys"])

# Vardas: Tomas, Pavardė: Rutkauskas
# lytis Vyras
# amzius 29
# daiktai ['Telefonas', 'Ausinės', 'Krepšys']
```
```python
def spausdinti_reiksmes(skaicius1, skaicius2, *args):
    print("Skaičių suma: ", skaicius1 + skaicius2)
    for vienas in args:
        print(vienas)


spausdinti_reiksmes(5, 2, "Labas", 5.26)

# Skaičių suma:  7
# Labas
# 5.26
```
## Globalūs ir lokalūs kintamieji
```python
globalus = 10

def funkcija():
    lokalus = 12
    suma = globalus + lokalus
    print(suma)

kita_suma = globalus + lokalus
print(kita_suma)
# NameError: name 'lokalus' is not defined

funkcija()
# 22
```
## Funkcijos komentavimas (Docstring)
```python
def funkcija(parametras1, parametras2):
    '''
    
    :param parametras1:
    :param parametras2:
    :return:
    '''
    return
def funkcija(parametras1, parametras2):
    '''
    Ši funkcija visiškai nieko nedaro
    :param parametras1: Nereikalingas parametras
    :param parametras2: Dar vienas nereikalingas
    parametras
    :return: Nieko negražina
    '''
    return
```
## Anoniminės (Lambda) funkcijos
Tai supaprastinta funkcija, paprastai naudojama tik kartą, visas kodas telpa vienoje eilutėje.

Paprastą funkciją:
```python
def kvadratu(a):
    return a ** 2
```
Galima pakeisti į:
```python
lambda a: a ** 2
```
Ją taip pat galima prisiskirti kintamajam ir iškviesti:
```python
kvadratu = lambda a: a ** 2

print(kvadratu(2))
```
Bet naudingiau panaudoti, pavyzdžiui, tokiu atveju:
```python
sarasas = [2, 5, 4, 65, 78, 99, 38]

sarasas2 = map(lambda a: a ** 2, sarasas)

for skaicius in sarasas2:
    print(skaicius)
```
Dar pora lambda panaudojimo pavyzdžių:
```python
daugyba_is_saves = [lambda i=skaicius: i*i for skaicius in range(1, 6)]
for vienas in daugyba_is_saves:
    print(vienas())
keliamieji = [lambda i=metai: i for metai in range(1900, 2101) if (metai % 400 == 0) or (metai % 100 != 0 and metai % 4 == 0)]
for vienas in keliamieji:
    print(vienas())
```
# Užduotys
## 1 užduotis
Sukurkite ir išsibandykite funkcijas, kurios:

* Gražinti trijų paduotų skaičių sumą.
* Gražintų paduoto sąrašo iš skaičių, sumą.
* Atspausdintų didžiausią iš kelių paduotų skaičių (panaudojant *args).
* Gražintų paduotą stringą atbulai.
* Atspausdintų, kiek paduotame stringe yra žodžių, didžiųjų ir mažųjų raidžių, skaičių.
* Gražintų sąrašą tik su nepasikartojančiais paduoto sąrašo elementais.
* Gražintų, ar paduotas skaičius yra pirminis.
* Išrikiuotų paduoto stringo žodžius nuo paskutinio iki pirmojo
* Gražina, ar paduoti metai yra keliamieji, ar ne.
* Atspausdina, kiek nuo paduotos sukakties praėjo metų, mėnesių, dienų, valandų, minučių, sekundžių.
## 2 užduotis
* Sukurti funkciją, kuri patikrintų, ar paduotas Lietuvos piliečio asmens kodas yra validus.
* Padaryti, kad programa sugeneruotų teisingą asmens kodą (panaudojus anksčiau sukurtą funkciją) pagal įvestą lytį, gimimo datą ir eilės numerį).

 (https://lt.wikipedia.org/wiki/Asmens_kodas) 
