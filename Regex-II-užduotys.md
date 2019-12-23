#1\
parašykite funkciją, kuri įvestą datą (formatas dd.mm.yyyy) keistų į yyyy mm dd. 
Dėl datų logikos nesirūpinkite, dirbame grynai su tekstu.

#2\
 ```python
text = '''Workshop & Tutorial proposals: November 21, 2019
Notification of acceptance: December 1, 2019
Workshop & Tutorial websites online: December 18, 2019
Workshop papers: February 28, 2020
Workshop paper notifications: March 27, 2020
Workshop paper camera-ready versions: April 10, 2020
Tutorial material due (online): April 10, 2020'''
```
Iš šio teksto atspausdinkite datų sąrašą.

#3\ 
Atspausdinkite tą patį teksta taip:

```python
# 1.
# Event: Workshop & Tutorial proposals due
# Date: November 21, 2019

# 2.
# Event: Notification of acceptance
# Date: December 1, 2019

# ir t.t.
```

#4\ 
Parašykite funkciją, kuri į parametrus priimtų teksta ir žodžių, kuriuos reikia jame išcenzūruoti sąrašą.
Pvz, žodis "kvaraba" yra baisus keiksmažodis, ir mums reikia duotame tekste pakeisti k*****a. 
Pradėkite maždaug taip:
```python
def cenzura(tekstas, *keiksmai):
    # čia bus jūsų funkcija

# iškvietus funkciją, pvz.:
cenzura('baisūs žodžiai, tokie kaip kvaraba, žaltys..', 'kvaraba', 'žaltys')
# mums atspausdintų
# baisūs žodžiai, tokie kaip k*****a, ž****s..
```
žodžių cenzūravimui naudokite regex, o jų sukeitimui tekste naudokite *.replace()*\
#5

Išsaugokite visą tekstą iš nuorodos į failą:
https://raw.githubusercontent.com/robotautas/kursas/master/RegEx/most_visited.html

čia yra html fragmentas, kuriame sudėti lankomiausi puslapiai 2019. 
Ištraukite šių puslapių sąrašą regex pagalba.

