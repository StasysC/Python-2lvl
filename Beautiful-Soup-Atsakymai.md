# 1

```python
import requests
from bs4 import BeautifulSoup
from random import shuffle

html = requests.get('http://delfi.lt').text
soup = BeautifulSoup(html, "html.parser")

title_tags = soup.select('.CBarticleTitle')
titles = [i.get_text() for i in title_tags]
bad_words = ['COVID', 'mirt', 'NVSC', 'skiep']

first_parts = []
second_parts = []
for title in titles:
     if ':' in title:
         if not any(word in title for word in bad_words):
             splitted = title.split(":")
             first_parts.append(splitted[0])
             second_parts.append(splitted[1])

shuffle(second_parts)

for i in range(len(first_parts)):
    print(first_parts[i], ":", second_parts[i])
```
# 2
```python
import requests
from bs4 import BeautifulSoup
from time import sleep
from random import randint


url = 'http://quotes.toscrape.com'
r = requests.get(url)

soup = BeautifulSoup(r.text, "html.parser")

# citatos
quotes_spans = soup.select('.text')
quotes_list = [i.get_text() for i in quotes_spans]

# nuorodos
a_blocks = soup.find_all('a', attrs={'class': None})
hrefs = [i['href'] for i in a_blocks if i.get_text()=="(about)"]

# atsakymai
author_blocks = soup.find_all('small', class_='author')
answers = [i.get_text() for i in author_blocks]

# uzuominos1
hints1 = []
for i in answers:
    splitted = i.split()
    hint = ''
    for i in splitted:
        if '.' not in i:
            hint += f'{i[0]}.'
        else:
            hint += i
    hints1.append(hint)

# uzuominos2
def get_second_hint(i):
    r = requests.get(url + hrefs[i])
    print(hrefs[i])
    soup = BeautifulSoup(r.text, "html.parser")
    text = soup.select('p')[1].get_text()
    return text

# žaidimo ciklas
while True:
    i = randint(1,10)
    print('\n',quotes_list[i])
    answer1 = input('Your answer: ')
    if answer1 != answers[i]:
        print(hints1[i])
        answer2 = input('Your answer: ')
        if answer2 != answers[i]:
            print(get_second_hint(i))
            answer3 = input('Your answer: ')
            if answer3 != answers[i]:
                if_continue = input(f'Correct answer is {answers[i]}. Continue? y/n: ')
                if if_continue == 'y':
                    continue
                else:
                    break
```