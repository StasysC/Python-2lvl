# Beautiful Soup

Beautiful Soup yra Python biblioteka, duomenų traukimui iš HTML ir XML. BS moka naviguoti tekste pagal html blokus, klases, id ar kitus atributus. Vienas iš populiariausių įrankių web scraping užduotims atlikti. Dokumentaciją rasite [čia](https://www.crummy.com/software/BeautifulSoup/bs4/doc/#quick-start). Diegiasi *pip install beautifulsoup4*.

```python
from bs4 import BeautifulSoup

html = """
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>First HTML Page</title>
</head>
<body>
  <div id="first">
    <h3 data-example="yes">hi</h3>
    <p>more text.</p>
  </div>
  <ol>
    <li class="special">This list item is special.</li>
    <li class="special">This list item is also special.</li>
    <li>This list item is not special.</li>
  </ol>
  <div data-example="yes">bye</div>
</body>
</html>
"""

soup = BeautifulSoup(html, "html.parser")
print(type(soup))
``` 

Importuojame BeautifulSoup klasę, ir iš HTML stringo išsiverdame buljoną :)
Dabar, turėdami *soup* objektą, galime naudotis jo funkcionalumu duomenų traukimui. Pvz.:

```python
print(soup.body)

# <body>
# <div id="first">
# <h3 data-example="yes">hi</h3>
# <p>more text.</p>
# </div>
# <ol>
# <li class="special">This list item is special.</li>
# <li class="special">This list item is also special.</li>
# <li>This list item is not special.</li>
# </ol>
# <div data-example="yes">bye</div>
# </body>
```

Ištraukiame *body* bloką. Arba:

```python
print(soup.body.div)

# <div id="first">
# <h3 data-example="yes">hi</h3>
# <p>more text.</p>
# </div>
```

Gavome pirmą div bloką bloke *body*. 

## find(), find_all()

Lygiai tą patį gautumėm panaudoję *.find()* metodą:

```python
print(soup.find('div'))

# <div id="first">
# <h3 data-example="yes">hi</h3>
# <p>more text.</p>
# </div>
```
*find()* ištraukia pirmą sutampančią atkarpą, *find_all* išgaudo visas ir grąžina sąraše:

```python
print(soup.find_all('div'))

# [<div id="first">
# <h3 data-example="yes">hi</h3>
# <p>more text.</p>
# </div>, <div data-example="yes">bye</div>]
```

Elementus taip pat galime traukti pagal bloko atributus, pvz *id, class* ir pan.:

```python
print(soup.find_all(class_='special'))

# [<li class="special">This list item is special.</li>, <li class="special">This list item is also special.</li>]
```
*Atkreipkite dėmesį, kaip užrašytas class_ parametras*

jeigu naudotumėm su unikaliais atributais, pvz *id* (HTML dokumente gali būti tik 1 unikalus id), analogiškai galime panaudoti metodą .find().

Jeigu ieškome pagal 'custom' atributus, pvz šiame dokumente *data-example="yes"*, naudosime tokią techniką:

```python
print(soup.find_all(attrs={'data-example': 'yes'}))

# [<h3 data-example="yes">hi</h3>, <div data-example="yes">bye</div>]
```

# Išrinkimas CSS stiliumi

Susipažinti su CSS selektoriais galite [čia](https://www.creativebloq.com/css3/introduction-css-selectors-61515320)

Naudosime metodą *.select()*:

```python
print(soup.select('#first'))

# [<div id="first">
# <h3 data-example="yes">hi</h3>
# <p>more text.</p>
# </div>]
```

Naudojant *select()*, visada gausime sąrašą, netgi jeigu jame tik vienas narys, todėl norėdami pasiekti konkretų jo narį turėsite nurodyti indeksą.

Dar keletas pavyzdžių:

```python
print(soup.select('.special'))

# [<li class="special">This list item is special.</li>, <li class="special">This list item is also special.</li>]
```

```python
print(soup.select('div'))

# [<div id="first">
# <h3 data-example="yes">hi</h3>
# <p>more text.</p>
# </div>, <div data-example="yes">bye</div>]
```

```python
print(soup.select('[data-example]'))

# [<h3 data-example="yes">hi</h3>, <div data-example="yes">bye</div>]
```

## get_text()

Kuomet norime ištraukti patį tekstą iš HTML bloko, darome taip:

```python
element = soup.select('.special')[0]
print(element.get_text())

# This list item is special.
```
Galime ir praiteruoti:

```python
elements = soup.select('.special')
for element in elements:
  print(element.get_text())

# This list item is special.
# This list item is also special.
```

## .name, .attrs

norėdami gauti blokų pavadinimus pagal (pvz) klasę, darysime taip:

```python
elements = soup.select('.special')
for element in elements:
  print(element.name)

# li
# li
```

norėdami išgauti bloko atributus, naudosime .attrs:

```python
elements = soup.select('meta')
print(elements[0].attrs)

# {'charset': 'UTF-8'}
```

Atributų reikšmes galime sužinoti tokiu būdu:

```python
attribute = soup.select('div')[0]['id']
print(attribute)

# first
```
arba:

```python
attribute = soup.find('div')['id']
print(attribute)

# first
```

## Navigacija tarp HTML elementų

### contents:

```python
print(soup.div.contents)

# ['\n', <h3 data-example="yes">hi</h3>, '\n', <p>more text.</p>, '\n']
```
būdas turi trūkumą, nes į sąrašą įtraukia naujos eilutės simbolius. Panagrinėkime html atkarpą:

```html
<body>
  <div id="first">
    <h3 data-example="yes">hi</h3>
    <p>more text.</p>
  </div>
  <ol>
    <li class="special">This list item is special.</li>
    <li class="special">This list item is also special.</li>
    <li>This list item is not special.</li>
  </ol>
  <div data-example="yes">bye</div>
</body>
```

*body* turi tris 'vaikus' - *div, ol, div*, vienas kitam jie yra 'broliai'(siblings), nes yra viename hierarchijos lygyje. 

```python
li = soup.find('li')
print(li.next_sibling.next_sibling) #todėl, kad '\n' užskaito už siblingą

# <li class="special">This list item is also special.</li>
```
suradome sekantį pirmojo *li* elemento 'brolį' (analogiškai galima dirbti su *previous_sibling*)

```python
print(li.parent)

# <ol>
# <li class="special">This list item is special.</li>
# <li class="special">This list item is also special.</li>
# <li>This list item is not special.</li>
# </ol>
```

išsiaiškinome, kas tėvas.

```python
print(li.parent.parent)

# <body>
# <div id="first">
# <h3 data-example="yes">hi</h3>
# <p>more text.</p>
# </div>
# <ol>
# <li class="special">This list item is special.</li>
# <li class="special">This list item is also special.</li>
# <li>This list item is not special.</li>
# </ol>
# <div data-example="yes">bye</div>
# </body>
```
sužinojome, kas senelis :)

Iki šiol navigavome per *Tags*, dabar pabandykime per metodus:

```python
li = soup.find('li')
print(li.find_next_sibling())

# <li class="special">This list item is also special.</li>
```

```python
li = soup.find('li')
print(li.find_next_siblings())

# [<li class="special">This list item is also special.</li>, <li>This list item is not special.</li>]
```

```python
# reikia suteikti klasę not-special paskutiniam li elementui
li = soup.find('li')
print(li.find_next_sibling(class_='not-special'))

# <li class="not-special">This list item is not special.</li>
```

## Kombinacijos

naviguojant galime kurti tokias ir panašias grandines:
```python
li = soup.find('li')
res = li.find_parent().find_previous_sibling()['id']
print(res)

# first
``` 
```python
res = soup.body.next_element.next_element.next_element.next_element.get_text()
print(res)

# hi
```

# Web scrapping pavyzdžiai
## Pavyzdys nr. 1
### Kaip nuskaityti norimą svetainės bloką (pirmą):
```python
from bs4 import BeautifulSoup
import requests

source = requests.get('https://www.delfi.lt/').text
soup = BeautifulSoup(source, 'html.parser')
blokas = soup.find('div', class_ = 'headline')
print(blokas.prettify())
```
### Kaip išrinkti norimą informaciją iš bloko:
```python
from bs4 import BeautifulSoup
import requests

source = requests.get('https://www.delfi.lt/').text
soup = BeautifulSoup(source, 'html.parser')
blokas = soup.find('div', class_ = 'headline')

kategorija = blokas.find('div', class_ = 'headline-category').text.strip()
tekstas = blokas.find('a', class_ = 'CBarticleTitle').text.strip()
linkas = blokas.find('a', class_="CBarticleTitle")['href']

print(kategorija)
print(tekstas)
print(linkas)
```
### Kaip gauti visų blokų informaciją:
```python
from bs4 import BeautifulSoup
import requests

source = requests.get('https://www.delfi.lt/').text
soup = BeautifulSoup(source, 'html.parser')
blokai = soup.find_all('div', class_ = 'headline')

for blokas in blokai:
    try:
        kategorija = blokas.find('div', class_ = 'headline-category').text.strip()
        tekstas = blokas.find('a', class_ = 'CBarticleTitle').text.strip()
        linkas = blokas.find('a', class_="CBarticleTitle")['href']
        print(kategorija)
        print(tekstas)
        print(linkas)
    except:
        pass
```
### Kaip įrašyti gautą informaciją į csv failą:
```python
from bs4 import BeautifulSoup
import requests
import csv

source = requests.get('https://www.delfi.lt/').text

soup = BeautifulSoup(source, 'html.parser')
blokai = soup.find_all('div', class_="headline")

with open("delfi_naujienos.csv", 'w', encoding="UTF-8", newline='') as failas:
    csv_writer = csv.writer(failas)
    csv_writer.writerow(['KATEGORIJA', 'ANTRAŠTĖ', 'NUORODA'])

    for blokas in blokai:
        try:
            kategorija = blokas.find("div", class_='headline-category').text.strip()
            tekstas = blokas.find('a', class_="CBarticleTitle").text.strip()
            linkas = blokas.find('a', class_="CBarticleTitle")['href']
            print(kategorija, tekstas, linkas)
            csv_writer.writerow([kategorija, tekstas, linkas])
        except:
            pass
```
### Daugiau rezultatų su regex:
```python
from bs4 import BeautifulSoup
import requests
import csv
import re

source = requests.get('https://www.delfi.lt/').text

soup = BeautifulSoup(source, 'html.parser')
blokai = soup.find_all('div', class_=re.compile(r'col-xs-.'))

with open("delfi_naujienos.csv", 'w', encoding="UTF-8", newline='') as failas:
    csv_writer = csv.writer(failas)
    csv_writer.writerow(['KATEGORIJA', 'ANTRAŠTĖ', 'NUORODA'])

    for blokas in blokai:
        try:
            kategorija = blokas.find("div", class_='headline-category').text.strip()
            tekstas = blokas.find('a', class_="CBarticleTitle").text.strip()
            linkas = blokas.find('a', class_="CBarticleTitle")['href']
            print(kategorija, tekstas, linkas)
            csv_writer.writerow([kategorija, tekstas, linkas])
        except:
            pass
```
## Pavyzdys Nr. 2
### Norimo gamintojo parduodamų telefonų išrinkimas iš svetainės
```python
import csv

from bs4 import BeautifulSoup
import requests

source = requests.get('https://www.telia.lt/prekes/mobilieji-telefonai/samsung').text
soup = BeautifulSoup(source, 'html.parser')

blokai = soup.find_all('div', class_ = 'mobiles-product-card card card__product card--anim js-product-compare-product')

with open("Telia Samsung telefonai.csv", "w", encoding="UTF-8", newline='') as failas:
    csv_writer = csv.writer(failas)
    csv_writer.writerow(['Modelis', 'Mėnesio kaina', 'Kaina'])

    for blokas in blokai:
        try:
            pavadinimas = blokas.find('a', class_ = 'mobiles-product-card__title js-open-product').text.strip()
            men_kaina = blokas.find('div', class_ = 'mobiles-product-card__price-marker').text.strip()
            kaina = blokas.find_all('div', class_ = 'mobiles-product-card__price-marker')[1].text.strip()
            print(pavadinimas, men_kaina, kaina)
            csv_writer.writerow([pavadinimas, men_kaina, kaina])
        except:
            pass
```
