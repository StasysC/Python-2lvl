Iteratorius - objektas, kurį galima iteruoti. Tai objektas, kuris grąžina duomenis,
kas kartą naudojant metodą next().

Iteratorius galima kurti iš bet kokių objektų, kuriuos galime iteruoti su for ciklais, 
pvz.: string, list, dict ir t.t.

Tarkime žodis "Kėdė" yra objektas iš kurio galime sukurti iteratorių:

```python
iteratorius = iter("Kėdė")
print(type(iteratorius))

# <class 'str_iterator'>
```

kai tik bus iškviestas iteratoriaus metodas next(), jis grąžins sekantį iteruojamo 
objekto segmentą, kol nebeliks ko iteruoti ir išmes StopIteration error:

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

Atkreipkite dėmesį, kaip iteratorius įsimena savo būseną(state), ir žino, 
kad reikia spausdinti sekantį simbolį. Mūsų nuolat naudojami *for* ciklai 
yra sukurti iteratorių pagrindu. Parašykime primityvų for ciklą:

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