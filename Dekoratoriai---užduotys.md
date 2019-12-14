1. Parašykite dekoratorių kuris riboja parametrų kiekį 
(tarkime, ne daugiau negu 2 parametrai funkcijai)
2. Parašykite dekoratorių, kuris leidžia į funkciją įrašyti tik string tipo parametrus.

3. Turime tokį kodą:
```python
import requests  # importuojame requests
from time import time  # importuojame time modulį

start_time = time()  # fiksuojame starto laiką
r = requests.get('http://www.cnn.com')  # sukuriame http užklausą
print(r.status_code)  # spausdiname status code (200 = OK, 404 = Not Found, ir t.t. galima pasiguglinti http status codes)
end_time = time()  # fiksuojame pabaigos laiką
print(end_time - start_time)  # atspausdiname laiką, per kurį gaovme atsakymą
```

Parašykite dekoratorių, bet kokios funkcijos vykdymo laikui fiksuoti. Galite patobulinti,
pvz funkcijos (vardas), su tokiais ir tokiais argumentais vykdymo laikas - XX s. 