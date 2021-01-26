# API's atsakymai

# 1
```python
import requests

url = 'https://api.frankfurter.app/'

def get_currency_list():
    r = requests.get(f'{url}currencies')
    dictionary = r.json()
    currency_list = []
    for key in dictionary.keys():
        currency_list.append(key)
    return currency_list


def get_rate(base, to):
    if base in get_currency_list() and to in get_currency_list():
        payload = {'from': base, 'to': to}
        r = requests.get(f'{url}latest', params=payload)
        dictionary = r.json()
        print(f'{dictionary["base"]}-{to}:\t{dictionary["rates"][to]}')
    else:
        print(f'''
Neteisingai suvestos valiutos. Galimų variantų sąrašas:
{get_currency_list()}
''')

get_rate('ZZZ', 'GBP')
```
# 2
```python
import requests
import webbrowser as wb

url = 'http://www.recipepuppy.com/api/'

def get_recipes(query):
    payload = {'q': query}
    r = requests.get(f'{url}', params=payload)
    response = r.json()
    for recipe in response['results']:
        with open(f'{query}.html', 'a') as html:
            html.write(f'''
<a href="{recipe['href']}">{recipe['title']}</a></br>
<img src="{recipe['thumbnail']}"></br></br>
            ''')
    wb.open_new_tab(f'{query}.html')
    # os.remove(f'{query}.html')

get_recipes('salmon')
```


# 3
```python
import requests
import json

url = 'https://api.frankfurter.app/'

def get_key(val, dct):
    """Little key by value extractor"""
    for k, v in dct.items():
        if val == v:
            return k


def currency_pair_analysis(base, to, start_date, end_date):
    payload = {'from': base, 'to': to}                                      # susikuriame parametrų žodyną
    r = requests.get(f'{url}{start_date}..{end_date}', params=payload)      # susikuriame užklausą pagal API dokumentaciją
    result = json.loads(r.text)                 # Atsakymą paverčiame Python žodynu
    new_dict = {}                               # Susikuriame tuščią žodyną
    for k, v in result['rates'].items():        # Užpildome jį reikšmėmis 'data': 'kursas'
        new_dict[k] = v[to]

    values_list = list(new_dict.values())       # Susikuriame kursų sąrašą
    min_value = min(values_list)                # Ištraukiame žemiausią reikšmę
    max_value = max(values_list)                # Ištraukiame aukščiausią reikšmę
    min_date = get_key(min_value, new_dict)     # Panaudojame pagalbinę funkciją rakto pagal reikšmę paieškai (gauname datą)
    max_date = get_key(max_value, new_dict)     # Gauname kitą datą

    ''' Formuojame Atsakymą:'''

    print(f'''
    Valiutų poroje {base}-{to}, periode nuo {start_date} iki {end_date}:
    Žemiausias kursas buvo {min_date} - {min_value}
    Aukščiausias kursas buvo {max_date} - {max_value}
    ''')

currency_pair_analysis('EUR', 'USD', '2015-01-01', '2015-01-10')

    # Valiutų poroje EUR-GBP, periode nuo 2019-01-01 iki 2019-12-31:
    # Žemiausias kursas buvo 2019-12-09 - 0.84116
    # Aukščiausias kursas buvo 2019-08-12 - 0.92203

```