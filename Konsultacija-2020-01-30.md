### Užduotis

turime eilutę su daug ip adresų:

```python
adresai = '122.35.203.161 174.217.10.111 187.121.176.91 176.114.85.116 174.59.204.133 54.209.112.174 109.185.143.49 176.114.253.216 210.171.87.76 24.169.250.142 2602:302:d13a:f530:f4ae:fa70:f110:286 150.29.94.236 103.58.98.120 174.36.99.77 174.119.230.231 174.154.138.251 210.186.27.182 174.66.239.72 1.116.93.232 93.7.15.104 186.107.159.98 109.185.43.38 63.241.146.31 174.59.35.159 213.107.185.54 213.107.185.54 150.162.174.78 178.212.99.206 1.243.213.10 64.18.100.185 174.62.241.161 37.230.204.191 91.120.76.65 34.207.134.209 109.156.141.56 174.137.147.90 24.128.231.111 186.241.37.20 109.62.14.183 150.130.64.133 174.146.173.75 109.112.44.214 210.210.230.92 174.118.64.94 188.233.41.255 156.168.58.204 178.21.3.57 192.227.116.16 210.210.230.92 174.118.64.94 188.233.41.255 156.168.58.204 178.21.3.57 192.227.116.16 109.247.192.231 109.224.21.212 91.176.62.12 91.73.35.54 156.96.61.107 174.248.220.79 1.156.218.42 174.59.14.41 109.100.43.189 210.235.177.198 1.13.235.181 186.203.212.26 68.65.122.170 50.113.36.224 209.161.96.253 102.128.76.219 209.95.42.177 209.95.42.177 174.60.83.83 191.102.104.105 210.171.155.156 74.198.158.40 174.20.35.139 191.173.114.151 187.150.190.131 196.31.46.173 14.124.229.252 1.116.184.108 47.208.153.78 150.29.37.130 161.142.16.180 109.116.212.180 109.173.153.132 94.103.96.132 1.160.170.61 79.151.247.174 174.123.63.12 5.237.167.182 105.112.106.108 109.116.57.99'
```

Sugeneruokite CSV failą, kuriame būtų stulpeliai IP,Country,City,Temp,Weather. Atidarius Excel ar kitoje lentelių skaityklėje, matytumėm maždaug tokį vaizdą:

![](https://github.com/robotautas/kursas/blob/master/konsultacijos/0130/ip_weather.png)

Naudokite šias API:

https://freegeoip.app/
https://api.met.no/weatherapi/locationforecast/2.0/documentation

Hints:

* Orų API duoda ypatingai išsamų JSON rezultatą. Tam kad susigaudyti, kaip išsitraukti reikšmes, naudokite
online JSON formatter'į, pvz.: https://jsonformatter.org/json-pretty-print. Mus domina pati pirma "air_temperature" reikšmė ir pati pirma "weather" reikšmė.

* Jeigu nežinote, kaip rašyti į CSV failus:

```python
import csv

with open('ip_data.csv', 'a') as f: # nurodome failo pavadinimą, ir kad norėsime rašyti 'append' būdu
        writer = csv.writer(f, delimiter=',') # susikuriame 'writer' objektą, nurodome kur rašysime, ir kad skirtukais bus kablelis
        writer.writerow(['IP', 'Country', 'City', 'Temp', 'Weather']) # objekto 'writerow' metodui perduodame iš esmės bet kokį sąrašą.
```





 

