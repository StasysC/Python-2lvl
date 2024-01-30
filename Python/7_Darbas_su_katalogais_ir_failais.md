# Darbas su failais ir katalogais (os modulis)
```python
import os
```
Kaip pažiūrėti, ką gali os modulis:
```python
print(dir(os))
```
Kaip sužinoti katalogą, kuriame esame:
```python
print(os.getcwd())

# C:\Users\Donoras\PycharmProjects\failai
```
Kaip pakeisti aktyvų katalogą, kuriame esame:
```python
os.chdir('C:\\Users\\Donoras\\Desktop')
print(os.getcwd())

# C:\Users\Donoras\Desktop
```
Kaip pažiūrėti, kokie failai ir katalogai yra kataloge:
```python
print(os.listdir())

# ['Demo katalogas', 'paveikslelis.jpg', 'tekstas.txt']
```
Kaip sukurti naują katalogą:
```python
os.mkdir("Naujas katalogas")
```
arba:
```python
os.makedirs("Naujas katalogas/Katalogas kataloge")

print(os.listdir())

# ['Demo katalogas', 'Naujas katalogas', 'paveikslelis.jpg', 'tekstas.txt']
```
Kaip sužinoti failo/katalogo informaciją:
```python
print(os.stat("Demo Katalogas"))
```
arba:
```python
print(os.stat("naujas_tekstas.txt"))

# os.stat_result(st_mode=33206,
# st_ino=11258999068714091, st_dev=987816996,
# st_nlink=1, st_uid=0, st_gid=0, st_size=279,
# st_atime=1553103727, st_mtime=1553072965,
# st_ctime=1553101362)
```
Kaip sužinoti failo dydį:
```python
print(os.stat("naujas_tekstas.txt").st_size)

# 279 (baitais)
```
Kaip sužinoti kada failas buvo paskutinį kartą modifikuotas:
```python
print(os.stat("naujas_tekstas.txt").st_mtime)

# 1553072965.1983721
```
Pakeitus suprantamu formatu:
```python
from datetime import datetime
data = os.stat("naujas_tekstas.txt").st_mtime
print(datetime.fromtimestamp(data))

# 2019-03-20 11:09:25.198372
```
# Tekstinių failų kūrimas ir nuskaitymas
Kaip sukurti tekstinį failą: (jei failo nėra, bus sukurtas naujas, jei yra - bus įrašoma jame)
```python
with open("failas.txt", 'w') as failas:
    failas.write("Sveikas, pasauli!")
```
arba (kitas būdas, kurio geriau nenaudoti):
```python
failas = open("failas.txt", 'w')
failas.write("Sveikas, pasauli!")
failas.close()
Kaip nuskaityti tekstą iš failo:

with open("failas.txt", 'r') as failas:
    print(failas.read())

# Sveikas, pasauli!
```
Kaip įrašyti ir nuskaityti failą vienu metu:
```python
with open("failas.txt", 'r+') as failas:
    print(failas.read())
    failas.write("Labas rytas, pasauli!")

# Sveikas, pasauli!

with open("failas.txt", 'r') as failas:
    print(failas.read())

# Sveikas, pasauli!Labas rytas, pasauli!
```
Kaip į failą įrašyti lietuviškus rašmenis: Problema:
```python
with open("failas.txt", 'w') as failas:
    failas.write("Čia yra pirmas failo sakinys")

# UnicodeEncodeError: 'charmap' codec can't encode character '\u010c' in position 0: character maps to <undefined>
```
Sprendimas:
```python
with open("failas.txt", 'w', encoding="utf-8") as failas:
    failas.write("Čia yra pirmas failo sakinys")
```
Kaip nuskaityti failą su lietuviškais rašmenimis:
```python
with open("failas.txt", 'r') as failas:
    print(failas.read())
```
```python
with open("failas.txt", 'r', encoding="utf-8") as failas:
    print(failas.read())
```
Kaip pridėti, o ne perrašyti failo eilutę:

Problema:
```python

with open("failas.txt", 'w', encoding="utf-8") as failas:
    failas.write("Čia yra pirmas sakinys \n")

with open("failas.txt", 'w', encoding="utf-8") as failas:
    failas.write("Čia yra antras sakinys \n")
```
Sprendimas:
```python
with open("failas.txt", 'a', encoding="utf-8") as failas:
    failas.write("Čia yra pirmas sakinys \n")

with open("failas.txt", 'a', encoding="utf-8") as failas:
    failas.write("Čia yra antras sakinys \n")
```
Kaip perrašyti tekstą norimoje vietoje:
```python
with open("failas.txt", 'w', encoding="utf-8") as failas:
    failas.write("Test")
    failas.write("Test")
```
```python
with open("failas.txt", 'w', encoding="utf-8") as failas:
    failas.write("Test")
    failas.seek(0)
    failas.write("BE")
```
Kaip nuskaityti failą po vieną eilutę:
```python
Čia yra pirmas sakinys
Čia yra antras sakinys
Čia yra trečias sakinys
Čia yra ketvirtas sakinys
Čia yra penktas sakinys
Čia yra šeštas sakinys
Čia yra septintas sakinys
Čia yra aštuntas sakinys
Čia yra devintas sakinys
Čia yra dešimtas sakinys
```
```python
with open("failas.txt", 'r', encoding="utf-8") as failas:
    print(failas.readline())
    print(failas.readline())
    print(failas.readline())

# Čia yra pirmas sakinys
# Čia yra antras sakinys
# Čia yra trečias sakinys
```
arba:
```python
with open("failas.txt", 'r', encoding="utf-8") as failas:
    print(failas.readlines())

# ['Čia yra pirmas sakinys \n', 'Čia yra antras sakinys \n', 'Čia
# yra trečias sakinys \n', 'Čia yra ketvirtas sakinys \n', 'Čia yra
# penktas sakinys \n', 'Čia yra šeštas sakinys \n', 'Čia yra septintas
# sakinys \n', 'Čia yra aštuntas sakinys \n', 'Čia yra devintas sakinys \
# n', 'Čia yra dešimtas sakinys \n']
```
Iteravimas per failo eilutes:
```python
with open("failas.txt", 'r', encoding="utf-8") as failas:
    for eilute in failas:
        print(eilute)

# Čia yra pirmas sakinys

# Čia yra antras sakinys

# Čia yra trečias sakinys

# Čia yra ketvirtas sakinys
```

kad nebūtų tarpų tarp eilučių:
```python
with open("failas.txt", 'r', encoding="utf-8") as failas:
    for eilute in failas:
        print(eilute, end="")

# Čia yra pirmas sakinys
# Čia yra antras sakinys
# Čia yra trečias sakinys
# Čia yra ketvirtas sakinys
# Čia yra penktas sakinys
# Čia yra šeštas sakinys
# Čia yra septintas sakinys
# .............
```

Kaip nuskaityti ribotą kiekį duomenų:
```python

with open("failas.txt", 'r', encoding="utf-8") as failas:
    print(failas.read(100))

# Čia yra pirmas sakinys
# Čia yra antras sakinys
# Čia yra trečias sakinys
# Čia yra ketvirtas sakinys

print(failas.read(100))

# Čia yra penktas sakinys
# Čia yra šeštas sakinys
# Čia yra septintas sakinys
# Čia yra aštuntas sakinys

print(failas.read(100))

# Čia yra devintas sakinys
# Čia yra dešimtas sakinys
```
Darbas su dviem failais (teksto kopijavimas iš vieno į kitą):
```python
with open("failas.txt", 'r') as r_failas:
    with open("failo_kopija.txt", 'w') as w_failas:
        for r_eilute in r_failas:
            w_failas.write(r_eilute)
```
(gauname tekstinio failo kopiją)

## Dvejetainių failų kopijavimas:

Problema:
```python
with open("logo.png", 'r') as r_failas:
    with open("logo_kopija.png", 'w') as w_failas:
        for r_eilute in r_failas:
            w_failas.write(r_eilute)

# UnicodeDecodeError: 'charmap' codec can't decode byte 0x9d in position 65: character maps to <undefined>
```
Sprendimas:
```python
with open("logo.png", 'rb') as r_failas:
    with open("logo_kopija.png", 'wb') as w_failas:
        for r_eilute in r_failas:
            w_failas.write(r_eilute)
```
(gauname paveikslėlio failo kopiją)

# Kaip į failą išsaugoti kintamuosius/objektus
(modulis pickle)

## Išsaugome kintamąjį
Įrašymas:
```python
import pickle

a = 1024

with open("a.pkl", "wb") as pickle_out:
    pickle.dump(a, pickle_out)
```
Nuskaitymas:
```python
import pickle

with open("a.pkl", "rb") as pickle_in:
    naujas_a = pickle.load(pickle_in)

print(naujas_a)

# 1024
```
## Išsaugome masyvą:
Įrašymas:
```python
import pickle

zodynas = {1:"Pirmas", 2:"Antras", 3:"Trečias"}

with open("zodynas.pkl", "wb") as pickle_out:
    pickle.dump(zodynas, pickle_out)
```
Nuskaitymas:
```python
import pickle

with open("zodynas.pkl", "rb") as pickle_in:
    naujas_zodynas = pickle.load(pickle_in)

print(naujas_zodynas)

# {1: 'Pirmas', 2: 'Antras', 3: 'Trečias'}
```
## Išsaugome daug kintamųjų (Pickle):
Įrašymas:
```python
a = 10
b = 7
c = 23

with open("abc.pkl", "wb") as pickle_out:
    pickle.dump(a, pickle_out)
    pickle.dump(b, pickle_out)
    pickle.dump(c, pickle_out)
```
Nuskaitymas:
```python
with open("abc.pkl", "rb") as pickle_in:
    nauja_a = pickle.load(pickle_in)
    nauja_b = pickle.load(pickle_in)
    nauja_c = pickle.load(pickle_in)

print(nauja_a)
print(nauja_b)
print(nauja_c)

# 10
# 7
# 23
```
arba:
```python
import pickle

with open("abc.pkl", "rb") as pickle_in:
    while True:
        try:
            print(pickle.load(pickle_in))
        except EOFError:
            break

# 10
# 7
# 23
```
Pavyzdys su vardų sąrašu:
```python
import pickle

while True:
    veiksmas = int(input("Pasirinkite: 1 - peržiūrėti, 2 - įrašyti, 3 - išeiti"))
    if veiksmas == 1:
        try:
            with open("zmones.pkl", 'rb') as file:
                print(pickle.load(file))
        except:
            print("Neįrašyta žmonių vardų")
    if veiksmas == 2:
        try:
            with open("zmones.pkl", 'rb') as file:
                zmones = pickle.load(file)
        except:
            zmones = []
        vardas = input("Įveskite naują vardą: ")
        zmones.append(vardas)
        with open("zmones.pkl", 'wb') as file:
            pickle.dump(zmones, file)
    if veiksmas == 3:
        print("Viso gero")
        break
```
Pavyzdys su objektų sarašu:
```python
import pickle

class Automobilis:
    def __init__(self, marke, modelis):
        self.marke = marke
        self.modelis = modelis

automobiliai = [Automobilis("Toyota", "Avensis"), Automobilis("Toyota", "Corolla"), Automobilis("Toyota", "Camry")]

with open("automobilis.pkl", "wb") as failas:
    pickle.dump(automobiliai, failas)

with open("automobilis.pkl", "rb") as failas:
    automobiliai = pickle.load(failas)
    for automobilis in automobiliai:
        print("Markė", automobilis.marke)
        print("Modelis", automobilis.modelis)
```

# Užduotys
## 1 užduotis
Sukurti programą, kuri:

* Sukurtų failą „Tekstas.txt“ su pilnu tekstu, gauto python kode paleidus „import this“.
* Atspausdintų tekstą iš sukurto failo
* Paskutinėje sukurto failo eilutėje pridėtų šiandienos datą ir laiką
* Sunumeruotų teksto eilutes (kiekvienos pradžioje pridėtų skaičių).
* Sukurtame faile eilutę "Beautiful is better than ugly." pakeistų į "Gražu yra geriau nei bjauru."
* Atspausdintų visą failo tekstą atbulai
* Atspausdintų, kiek failo tekste yra žodžių, skaičių, didžiųjų ir mažųjų raidžių
* Nukopijuotų visą sukurto failą tekstą į naują failą, tik DIDŽIOSIOMIS RAIDĖMIS
Patarimai:

* Naudoti from datetime import datetime, datetime.today()
* Kintamajam priskirti sakinį, kuriuo bus operuojama, eilutėmis
* Kai kur galima panaudoti funkcijas iš praeitų pamokų

Galima panaudoti 4 užduotyje:
```python
sarasas = ["Vienas", "Du", "Trys"]

for numeris, zodis in enumerate(sarasas, 1):
    print(numeris, zodis)

# 1
# Vienas
# 2
# Du
# 3
# Trys
```
## 2 užduotis
Sukurti programą, kuri:

* Leistų vartotojui įvesti norimą eilučių kiekį
* Leistų vartotojui įrašyti norimą kuriamo failo pavadinimą
* Įrašytų įvestą tekstą atskiromis eilutėmis į failą
  
Patarimai:

Sukurti while ciklą, kuris užsibaigtų tik įvedus vartotojui tuščią eilutę (nuspaudus ENTER)
## 3 užduotis
Sukurti programą, kuri:

* Kompiuterio darbalaukyje (Desktop) sukurtų katalogą „Naujas Katalogas“
* Šiame kataloge sukurtų tekstinį failą, kuriame būtų šiandienos data ir laikas
* Atspausdintų šio tekstinio failo sukūrimo datą ir dydį baitais
Patarimai:

* Failo sukūrimo datą galima pasiekti per os.stat(„Failas.txt“).st_ctime
## 4 užduotis
Sukurti minibiudžeto programą, kuri:

* Leistų vartotojui įvesti pajamas arba išlaidas (su "-" ženklu)
* Pajamas ir išlaidas saugotų sąraše, o sąrašą pickle faile (uždarius programą, įvesti duomenys nedingtų)
* Atvaizduotų jau įvestas pajamas ir išlaidas
* Atvaizduotų įvestų pajamų ir išlaidų balansą (sudėtų visas pajamas ir išlaidas)

Patarimas:
```python
import pickle
```
