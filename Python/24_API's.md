# API

API (*Application Programming Interface*) - Aplikacijų programavimo sąsaja, aukštesnio lygio abstrakcijos lygmuo, 
leidžiantis programuotojui išnaudoti tam tikrą funkcionalumą. Pvz - visos operacinės sistemos turi API, todėl 
programuotojas gali kurti programas, kurias OS paskui vykdo. Šiandien kalbėsime apie pačias paprasčiausias - web API's.
Web API priima užklausą ir grąžina rezultatą, dažniausiai JSON formatu. Su tuo rezultatu paskui galime daryti ką norime
(panaudoti savo web programėlėje, išsaugoti duomenų bazėje ir t.t.)

```python
import requests

people = requests.get('http://api.open-notify.org/astros.json')
print(people.text)

# {"people": [{"name": "Christina Koch", "craft": "ISS"}, {"name": "Alexander Skvortsov", "craft": "ISS"}, 
# {"name": "Luca Parmitano", "craft": "ISS"}, {"name": "Andrew Morgan", "craft": "ISS"}, 
# {"name": "Oleg Skripochka", "craft": "ISS"}, {"name": "Jessica Meir", "craft": "ISS"}], "number": 6, "message": "success"}
```

Gauname JSON sąrašą žmonių, šiuo metu reziduojančių Tarptautinėje Kosminėje Stotyje.
API's dažniausiai turi savo dokumentaciją, kad žinotumėm, kaip pateikti užklausas norimam rezultatui gauti. Prieš naudojantis, 
verta pasiskaityti. \
Web API's yra labai daug, duomenis jos pateikia iš pačių įvairiausių gyvenimo sričių. 
[Šioje nuorodoje](https://github.com/public-apis/public-apis) rasite sąrašą nemokamų web API's. Dalis jų reikalauja 
registracijos ir autentifikacijos (*apiKey*), kitas galima naudoti tiesiog iš karto.

```python
import requests

headers = {"apikey": "KQVVznJtJA4eY4DBAk0cCGATHJ0BaHyF"}
months = ['01', '02', '03', '04', '05', '06', '07', '08', '09', '10', '11', '12']
for month in months:
    url = f"https://api.apilayer.com/exchangerates_data/2021-{month}-16?symbols=USD&base=EUR"
    response = requests.get(url, headers=headers)
    result = response.json()
    print(f"2021-{month}-15     EUR-USD    {result['rates']['USD']}")

# 2021-01-15     EUR-USD    1.20795
# 2021-02-15     EUR-USD    1.209212
# 2021-03-15     EUR-USD    1.190129
# 2021-04-15     EUR-USD    1.198195
# 2021-05-15     EUR-USD    1.215059
# 2021-06-15     EUR-USD    1.199379
# 2021-07-15     EUR-USD    1.180665
# 2021-08-15     EUR-USD    1.177854
# 2021-09-15     EUR-USD    1.176495
# 2021-10-15     EUR-USD    1.159911
# 2021-11-15     EUR-USD    1.131791
# 2021-12-15     EUR-USD    1.133472
```
 
 Šiame pavyzdyje matome, kaip nesudėtingai galime gauti EUR-USD kasmėnesinius kurso pokyčius. Rezultatą galime panaudoti 
 kur tik norime, atlikti papildomus skaičiavimus, braižyti grafikus, vaizduoti juos interneto tinklalapyje ir t.t.
 
 Kai kurios API paslaugas teikiančios svetainės reikalauja registracijos, tam, kad išvengtų piktnaudžiavimo, ir galėtų 
 taikyti įvairius apribojimus (užklausų per dieną ir t.t.). Jums užsiregisravus, gausite su jūsų duomenimis susietą *apiKey*, 
 kurį, priklausomai nuo dokumentacijos, turėsite nurodyti vykdydami užklausą.
 
 Pvz, užsiregistravus https://pixabay.com/ dokumentacijoje rasite jums priklausantį API raktą:
 ```python
import webbrowser as wb
import requests
import json

API_key = '14795746-624081efd179b5bd9be0efe43'


def open_first(query):
    payload = {'key': API_key, 'q': query, 'img_type': 'photo', 'pretty': 'true'}
    r = requests.get('https://pixabay.com/api/', params=payload)
    json_str = r.text
    result = json.loads(json_str)
    wb.open_new_tab(result['hits'][1]['largeImageURL'])

open_first('elephant')
```
Čia yra programėlė, kuri naršyklėje atidaro pirmą nuotrauką pagal paiešką. Dokumentacijoje nurodyta, 
kad API raktas turi būti nurodytas URL eilutės parametruose, ten jį ir įdėjome. 
[Webbrowser](https://docs.python.org/3/library/webbrowser.html) yra paprasta biblioteka, valdanti naršyklę.
Beje, neviešinkite savo API rakto, nes gali atsirasti piktnaudžiautojų, dėl kurių veiksmų jums gali būti 
apribota paslauga, kai kuriais atvejais (pvz. Google) išrašyta sąskaita. 

# Užduotys
## 1 užduotis
Sukurkite programą, kuri duoda įvestos valiutų poros dabartinį kursą. Naudokitės Frankfurter API. 
Dokumentaciją rasite [čia](https://www.frankfurter.app/docs/). Rezultatas galėtų atrodyti taip:
```python
get_rate('EUR', 'GBP')
# EUR-GBP:	0.84828

get_rate('ZZZ', 'GBP')
# Neteisingai suvestos valiutos. Galimų variantų sąrašas:
# ['AUD', 'BGN', 'BRL', 'CAD', 'CHF', 'CNY', 'CZK', 'DKK', 'EUR', 'GBP', 'HKD', 'HRK', 'HUF', 'IDR', 'ILS', 'INR', 'ISK', 'JPY', 'KRW', 'MXN', 'MYR', 'NOK', 'NZD', 'PHP', 'PLN', 'RON', 'RUB', 'SEK', 'SGD', 'THB', 'TRY', 'USD', 'ZAR']
```

## 2 užduotis
Naudodami tą pačią Frankfurter API (kaip ir pirmoje užduotyje), sukurkite programą, kuri pagal parametruose pateiktas valiutų poras, 
periodo pradžios ir pabaigos datą surastų dienas kai kursas buvo aukščiausias ir kai kursas buvo žemiausias
Maždaug taip:

```python
currency_pair_analysis('EUR', 'GBP', '2019-01-01', '2019-12-31')

    # Valiutų poroje EUR-GBP, periode nuo 2019-01-01 iki 2019-12-31:
    # Žemiausias kursas buvo 2019-12-09 - 0.84116
    # Aukščiausias kursas buvo 2019-08-12 - 0.92203
```

<!--
# 2
Sukurkite programą, kuri atspausdintų jūsų rytdienos horoskopą, naudokite šį [resursą](https://github.com/sameerkumar18/aztro).
-->

