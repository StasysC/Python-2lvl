# Kada gali prireikti get/set metodų?
```python
class Darbuotojas:
    def __init__(self, vardas, pavarde, atlyginimas):
        self.vardas = vardas
        self.pavarde = pavarde
        self.atlyginimas = atlyginimas

domas = Darbuotojas("Domas", "Rutkauskas", 1200)
domas.atlyginimas = 1500
print(domas.atlyginimas)
```
Problema
```python
domas = Darbuotojas("Domas", "Rutkauskas", 1200)
domas.atlyginimas = -150
print(domas.atlyginimas)
```
Variantas:
```python
class Darbuotojas:
    def __init__(self, vardas, pavarde, atlyginimas):
        self.vardas = vardas
        self.pavarde = pavarde
        self.__atlyginimas = atlyginimas

    def set_atlyginimas(self, naujas):
        if naujas < 0:
            print("Atlyginimas negali būti neigiamas")
        else:
            self.__atlyginimas = naujas

domas = Darbuotojas("Domas", "Rutkauskas", 1200)
domas.set_atlyginimas(-1200)

# Atlyginimas negali būti neigiamas

print(domas.atlyginimas)

# AttributeError: 'Darbuotojas' object has no attribute 'atlyginimas'
```
Galime sukurti ir getterį:
```python
class Darbuotojas:
    def __init__(self, vardas, pavarde, atlyginimas):
        self.vardas = vardas
        self.pavarde = pavarde
        self.__atlyginimas = atlyginimas

    def set_atlyginimas(self, naujas):
        if naujas < 0:
            print("Atlyginimas negali būti neigiamas")
        else:
            self.__atlyginimas = naujas

    def get_atlyginimas(self):
        return self.__atlyginimas

domas = Darbuotojas("Domas", "Rutkauskas", 1200)
print(domas.get_atlyginimas())

# 1200


domas.atlyginimas = 500
print(domas.get_atlyginimas())

# 1200
```
# Python būdas išspręsti geterių/seterių problemą
## Dekoratorius @Property:
```python
class Darbuotojas:
    def __init__(self, vardas, pavarde, atlyginimas):
        self.vardas = vardas
        self.pavarde = pavarde
        self.__atlyginimas = atlyginimas

    @property
    def atlyginimas(self):
        return self.__atlyginimas

    @atlyginimas.setter
    def atlyginimas(self, naujas):
        if naujas < 0:
            print("Atlyginimas negali būti neigiamas")
        else:
            self.__atlyginimas = naujas


domas = Darbuotojas("Domas", "Rutkauskas", 1200)
print(domas.atlyginimas)
# 1200

domas.atlyginimas = 1500
print(domas.atlyginimas)
# 1500

domas.atlyginimas = -150
# Atlyginimas negali būti neigiamas

print(domas.atlyginimas)
# 1500
```

# Debug
## Kintamųjų atvaizdavimas
![](https://github.com/StasysC/Python-2lvl/blob/master/Python/Kint1.png)

![](https://github.com/StasysC/Python-2lvl/blob/master/Python/kint2.png)
## Sąrašo debug
![](https://github.com/StasysC/Python-2lvl/blob/master/Python/SarasoDebug.png)
## Kodo tikrinimas
![](https://github.com/StasysC/Python-2lvl/blob/master/Python/KodoVeikimas.png)

![](https://github.com/StasysC/Python-2lvl/blob/master/Python/Kodoveikimas2.png)
## Objektų atvaizdavimas
![](https://github.com/StasysC/Python-2lvl/blob/master/Python/objektai.png)

# Užduotys
## 1 užduotis
Parašyti klasę "Namas", kuri turėtų savybę "plotas" ir "verte". Padaryti taip, kad savybė "verte" koreguojama tik įvedus skaičių. Programoje naudoti dekoratorių @property.
