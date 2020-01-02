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
months = ['01', '02', '03', '04', '05', '06', '07', '08', '09', '10', '11', '12']
for month in months:
    r = requests.get(f'https://api.ratesapi.io/api/2019-{month}-15')
    dictionary = json.loads(r.text)
    print(f"2019-{month}-15     EUR-USD    {dictionary['rates']['USD']}")

# 2019-01-15     EUR-USD    1.1424
# 2019-02-15     EUR-USD    1.126
# 2019-03-15     EUR-USD    1.1308
# 2019-04-15     EUR-USD    1.1313
# 2019-05-15     EUR-USD    1.1183
# 2019-06-15     EUR-USD    1.1265
# 2019-07-15     EUR-USD    1.1269
# 2019-08-15     EUR-USD    1.115
# 2019-09-15     EUR-USD    1.1096
# 2019-10-15     EUR-USD    1.1007
# 2019-11-15     EUR-USD    1.1034
# 2019-12-15     EUR-USD    1.1174
```
 
 Šiame pavyzdyje matome, kaip nesudėtingai galime gauti EUR-USD kasmėnesinius kurso pokyčius. Rezultatą galime panaudoti 
 kur tik norime, atlikti papildomus skaičiavimus, braižyti grafikus, vaizduoti juos interneto tinklalapyje ir t.t.
 
 Kai kurios API paslaugas teikiančios svetainės reikalauja registracijos, tam, kad išvengtų piktnaudžiavimo, ir galėtų 
 taikyti įvairius apribojimus (užklausų per dieną ir t.t.). Jums užsiregisravus, gausite su jūsų duomenimis susietą *apiKey*, 
 be kurį, priklausomai nuo dokumentacijos turėsite nurodyti, vykdydami užklausą.
 
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
[Webbrowser](https://docs.python.org/2/library/webbrowser.html) yra paprasta biblioteka, valdanti naršyklę.
Beje, neviešinkite savo API rakto, nes gali atsirasti piktnaudžiautojų, dėl kurių veiksmų jums gali būti 
apribota paslauga, kai kuriais atvejais (pvz. Google) išrašyta sąskaita. 