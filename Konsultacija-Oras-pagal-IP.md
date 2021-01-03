### Užduotis

turime eilutę su daug ip adresų:

```python
ip_list = ['122.35.203.161', '174.217.10.111', '187.121.176.91', '176.114.85.116', '174.59.204.133', '54.209.112.174', '109.185.143.49', '176.114.253.216', '210.171.87.76', '24.169.250.142']
```

Sugeneruokite CSV failą, kuriame būtų stulpeliai IP,Country,City,Temp,Weather. Atidarius Excel ar kitoje lentelių skaityklėje, matytumėm maždaug tokį vaizdą:

![](https://github.com/robotautas/kursas/blob/master/konsultacijos/0130/ip_weather.png)

Naudokite šias API:

* https://freegeoip.app/
* http://api.openweathermap.org/data/2.5/weather/

OpenWeather reikės užsiregistruoti ir gauti API-key.

* Jeigu nežinote, kaip rašyti į CSV failus:

```python
import csv

with open('ip_data.csv', 'a') as f: # nurodome failo pavadinimą, ir kad norėsime rašyti 'append' būdu
        writer = csv.writer(f, delimiter=',') # susikuriame 'writer' objektą, nurodome kur rašysime, ir kad skirtukais bus kablelis
        writer.writerow(['IP', 'Country', 'City', 'Temp', 'Weather']) # objekto 'writerow' metodui perduodame iš esmės bet kokį sąrašą.
```



 
# [ATSAKYMAS](https://github.com/robotautas/kursas/blob/master/konsultacijos/0130/sav_darbas.py)
