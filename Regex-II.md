Regex užklausas Python'e tvarko modulis *re*.
Prieš pradėdami darbą, nepamirškime importuoti:

```python
import re
```

tarkime, kad dirbsime su telefono numeriais, tokiais kaip +370 642 12321. Iš pradžių reikia susikurti šabloną 
(regex objektą):

```python
pattern = re.compile(r'\+370\s\d{3}\s\d{4}')
```

Kintamąjame *pattern* dabar turime objektą, kuris turi įvairių naudingų metodų iš re bibliotekos.
Pirmas iš jų, kurį galime pabandyti yra *search*:

```python
tekstas = '''Pirmas telefono numeris yra +370 123 12321, antras +370 321 10101.'''
res = pattern.search(tekstas)
print(res)

# <re.Match object; span=(28, 42), match='+370 123 12321'>
```

*res* dabar yra mūsų *Match* objektas. Atspausdinus jį matome, kad tekste yra šabloną atitinksnti simbolių seka,
kurios pradžios indeksas 28, pabaigos 42(neįskaitant). Metodas ieško ir grąžina pirmą surastą reikšmę. Jei *.search* neranda mūsų
šabloną atitinkančios simbolių sekos, gauname res įgauna *None* reikšmę.
Tam, kad ištraukti match reikšmę, naudojame *.group()* metodą:

```python
print(res.group())

# +370 123 12321
```

*search* metodas nepalaiko daugiau negu 1 reikšmės suradimo tekste, norint surasti visas, 
naudojamas metodas *findall*:

```python
res = pattern.findall(tekstas)
print(res)

#['+370 123 12321', '+370 321 10101']
```

*findall* grąžina surastus atitikmenis sąraše.

Parašykime paprastą funkciją, kuri patikrintų, ar pateiktas el. pašto adresas atitinka standartus:

```python
def validate_email(input):
    email_regex = re.compile(r'^[a-zA-Z0-9._%-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,6}$')
    result = email_regex.search(input)
    if result:
        return True
    return False

print(validate_email('kazkoks@email.lt'))
print(validate_email('neteisingas@@email.lt'))

# True
# False
```

Įsivaizduokite, kiek Python kodo reikėtų, norint parašyti analogišką funkciją nenaudojant regex :)

Kaip gauti naudos iš grupavimo? Tarkime, turime vardų sąrašą tokiu formatu - Mr. Phil Collins.
Parašykime funkciją, kuri išskaido kreipinį, vardą ir pavardę:

```python
def split_names(name):
    pattern = re.compile(r'^([A-Z]\w{1,3}\.)\s([A-Z]\w+)\s([A-Z]\w+)$')
    result = pattern.search(name)
    if result:
        print(f'Visa eilutė: {result.group(0)}')
        print(f'Kreipinys: {result.group(1)}')
        print(f'Vardas: {result.group(2)}')
        print(f'Pavardė: {result.group(3)}')
        print('----------------------------------')
        print(result.group())
        print(result.groups())
    else:
        print('Įvestis neatitinka šablono')

split_names('Mr. Clint Eastwood')

# Visa eilutė: Mr. Clint Eastwood
# Kreipinys: Mr.
# Vardas: Clint
# Pavardė: Eastwood
# ----------------------------------
# Mr. Clint Eastwood
# ('Mr.', 'Clint', 'Eastwood')
```

Kaip matome, metodas *group* įvedus nulį grąžina visą eilutę, o toliau įvedant reikšmes nuo 1, 
paeiliui grąžina atskiras grupes. Tuščias *group()* veikia kaip ir *group(0)*, o groups() 
grąžina grupes *tuple* masyve.

jeigu norime, grupėms galime suteikti savo pavadinimus, naudodami tokią sintaksę:

```python
pattern = re.compile(r'^(?P<kreipinys>[A-Z]\w{1,3}\.)\s([A-Z]\w+)\s([A-Z]\w+)$')
print(f'Kreipinys: {result.group("kreipinys")}')
```
Šiuo atveju nereikia sukti galvos, kelintoje grupėje mūsų norimas rezultatas.

RegEx galime pasitelkti ir simbolių eilučių pakeitimams. Tam naudojamas metodas re.sub():

```python
card_number = "card1: 0452 6544 0004 4456, card2: 1234 4567 8910 1112"
pattern = re.compile(r'\b\d{4}\s\d{4}\s\d{4}\s\d{4}\b')
res = pattern.sub('**** **** **** ****', card_number)
print(res)

# card1: **** **** **** ****, card2: **** **** **** ****
```

Jeigu norime palikti dalį originalios sekos, galime pasitelkti grupavimą, ir daryti taip:

```python
card_number = "card1: 0452 6544 0004 4456, card2: 1234 4567 8910 1112"
pattern = re.compile(r'\b(\d{4})\s\d{4}\s\d{4}\s\d{4}\b')
res = pattern.sub('\g<1> **** **** ****', card_number)
print(res)

# card1: 0452 **** **** ****, card2: 1234 **** **** ****
```

pattern.sub metode nurodytas '\\g<1> **** **** ****' argumentas yra mūsų pakeitimas, 
kuriame '\\g<1>' yra pirma grupė mūsų šablone. Ją paliekame nekeistą. likusią dalį 
pakeičiame '\*' simboliais. Antras argumentas yra tekstas su kuriuo dirbame.

<!--**...Čia dar bus re flags...**-->