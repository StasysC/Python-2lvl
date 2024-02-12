# Iteratoriai
Iteratorius - objektas, kurį galima iteruoti. Tai objektas, kuris grąžina duomenis, kas kartą naudojant metodą next().

Iteratorius galima kurti iš bet kokių objektų, kuriuos galime iteruoti su for ciklais, pvz.: string, list, dict ir t.t.

Tarkime žodis "Kėdė" yra objektas iš kurio galime sukurti iteratorių:
```python
iteratorius = iter("Kėdė")
print(type(iteratorius))

# <class 'str_iterator'>
```
kai tik bus iškviestas iteratoriaus metodas next(), jis grąžins sekantį iteruojamo objekto segmentą, kol nebeliks ko iteruoti ir išmes StopIteration error:
```python
print(next(iteratorius))
print(next(iteratorius))
print(next(iteratorius))
print(next(iteratorius))
print(next(iteratorius))

# K
# ė
# d
# ė
# Traceback (most recent call last):
#   File "/home/blablabla/iterators.py", line 8, in <module>
#     print(next(iteratorius))
# StopIteration
```
Atkreipkite dėmesį, kaip iteratorius įsimena savo būseną(state), ir žino, kad reikia spausdinti sekantį simbolį. Mūsų nuolat naudojami for ciklai yra sukurti iteratorių pagrindu. Parašykime primityvų for ciklą:
```python
numeriai = [1, 2, 3]

for num in numeriai:
    print(num)
    
# 1
# 2
# 3
```
O dabar tą pačią iteraciją atlikime be for sintaksės:
```python
iteratorius = iter(numeriai)
while True:
    try:
        print(next(iteratorius))
    except StopIteration:
        break
# 1
# 2
# 3
```
O dabar parašykime šiek tiek universalesnę funkciją:
```python
def iteruoklis(objektas, func):
    iteratorius = iter(objektas)
    while True:
        try:
            item = next(iteratorius)
        except StopIteration:
            break
        else:
            func(item)
```
Mūsų funkcija priima objektą (pvz. list'ą ar kt.) iš karto jį paverčia iteratoriumi. Tuomet, kol yra ką iteruoti, iteruoja ir praleidžia per mūsų funkciją argumentuose func. Pvz.:
```python
broliai = ['jurgis', 'antanas', 'aloyzas', 'martynas']
iteruoklis(broliai, print)

# jurgis
# antanas
# aloyzas
# martynas
```
Šiuo atveju pritaikėme Python integruotą funkciją print, taigi mums bus paprasčiausiai atspausdinti brolių vardai. Galime panaudoti savo sukurtą funkciją, tarkime:
```python
def kubu(x):
    print(x**3)

nums = [1, 2, 3, 4, 5]
iteruoklis(nums, kubu)

# 1
# 8
# 27
# 64
# 125
```

# Generatoriai

Generatoriai yra iteratorių rūšis. Jie yra paprastesnis būdas kurti iteratorius. Generatoriai kuriami naudojant generatorių funkcijas. Generatorių funkcijų ypatumas yra tas, kad vietoje return naudojame yield.
Skirtumai tarp paprastų ir generatoriaus funkcijų (generator functions):

| Funkcija                  | Generatoriaus funkcija              |
|---------------------------|-------------------------------------|
| naudoja return            | naudoja yield                       |
| grąžina rezultatą 1 kartą | gali grąžinti rezultatus daug kartų |
| grąžina *return* vertę    | grąžina generatorių                 |

Pvz.:

```python
def skaiciuojam_iki(iki):
    count = 1
    while count <= iki:
        yield count
        count +=1
```

čia yra generatoriaus funkcija. Iš jos galime susikurti generatorių ir analogiškai, 
kaip ir su kitais iteratoriais, galime iškvieti funkciją *next*:

```python
counter = skaiciuojam_iki(5)
print(next(counter))
print(next(counter))
print(next(counter))
print(next(counter))
print(next(counter))
print(next(counter))

# 1
# 2
# 3
# 4
# 5
# Traceback (most recent call last):
#   File "/home/blablabla/uzduotys.py", line 11, in <module>
#     print(next(counter))
# StopIteration
```
Kaip matome, veiksmas vyksta vienodai, kaip ir su iteratoriais, 
nes generatorius ir yra iteratorius.

Beje, generatorius galima paversti į list'us:

```python
sarasas = list(counter)
print(sarasas)
# [1, 2, 3]
```

Ir juos iteruoti su paprastais *for* ciklais:

```python
for i in counter:
    print(i)

# 1
# 2
# 3
```

o dabar padidinkime iki reikšmę iki 10 ir atlikim eksperimentą:

```python
counter = skaiciuojam_iki(10)
print(next(counter))
print(next(counter))
print(next(counter))
sarasas = list(counter)
print(sarasas)

# 1
# 2
# 3
# [4, 5, 6, 7, 8, 9, 10]
```

šis pavyzdys iliustruoja, kaip veikia generatoriai - jie nekaupia viso turinio atmintyje,
o tik įsidėmi momentinę reikšmę, kurios pagrindu generuoja sekančią. 1, 2, 3 reikšmės buvo 
panaudotos ir išmestos, o sąrašas suformuotas tik iš to, kas liko. Dėl to generatoriai 
veikia gerokai sparčiau už įprastus *for loops*.

Yra dar vienas metodas generatoriams kurti - *generator expressions*. 
Pamenate *list comprehension*?:) Tai yra analogiškas sintaksinis palengvinimas
kurti generatoriams. Pvz.:

```python
g = (num**2 for num in range(1, 50))
print(type(g))

print(next(g))
print(next(g))
print(next(g))
# ir t.t.

# <class 'generator'>
# 1
# 4
# 9
```
# Užduotys
## 1 užduotis
Parašykite generatorių, kuris kaskartą inicijuotas su funkcija next grąžintų sekantį porinį skaičių. Pirmas sk. 2, toliau 4 ir taip be pabaigos.
## 2 užduotis
Parašykite generatorų , kuris kas kartą generuotų po vieną Fibonačio sekos skaičių. (Seka prasideda šiais skaičiais: 0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, 144, 233. Kiekvienas šios sekos skaičius lygus dviejų prieš jį einančių skaičių sumai, daugiau google:)
## 3 užduotis
Įsivaizduokite, kad reikia nulaužti 4 skaitmenų pin kodą. Parašykite generatorių, kuris tikrins po viena kombinaciją, pradedant 0000, ir sustos, kai pin kodas bus teisingas. Pradėkite programą nuo (pvz.) PIN = '0549' ir rašykite toliau. Pabaigus funkciją, praiteruokite sukurtą generatorių su for ciklu, kad spausdintų skaičiukus iš eilės ir atspausdinus paskutinį, parašytų 'PIN is XXXX(jųsų pin'as)'. Atkreipkite dėmesį, kad kodas gali prasidėti nuliu. Sugalvokite, kaip apeiti šią problemą :).
## 4 užduotis
Parašykite generatoriaus funkciją, kuri atidarytų nurodytą failą, ir grąžintų po vieną eilutę (tiesiog yield'inti reikės ne skaičių o kitą duomenų tipą.). Reikės prisiminti darbą su failais :)
