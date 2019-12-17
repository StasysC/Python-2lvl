* Generatoriai yra iteratorių rūšis. Jie yra paprastesnis būdas kurti iteratorius;
* Generatoriai kuriami naudojant generatorių funkcijas;
* Generatorių funkcijų ypatumas yra tas, kad vietoje *return* naudojame *yield*;

skirtumai tarp paprastų ir generatoriaus funkcijų (generator functions):

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
