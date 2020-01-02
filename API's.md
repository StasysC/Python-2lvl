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
```
 
 Šiame pavyzdyje matome, kaip nesudėtingai galime gauti EUR-USD kasmėnesinius kurso pokyčius. Rezultatą galime panaudoti 
 kur tik norime, atlikti papildomus skaičiavimus, braižyti grafikus, vaizduoti juos interneto tinklalapyje ir t.t.