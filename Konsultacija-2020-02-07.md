## Arbitražas

Arbitražas yra paprasta prekybos strategija, kai vienoje vietoje perkama pigiau, o kitoje - padruodama brangiau.

## Užduotis

Jums reikės, naudojant [šį API](https://www.coinlore.com/cryptocurrency-data-api) parašyti flask programėlę, kuri sugeneruotų naršyklėje lentelę, kurioje matytųsi:

* Kriptovaliutos pavadinimas
* Keityklos, kuri tą kriptovaliutą siūlo pigiausiai, pavadinimas
* Kaina USD už vnt. (pirkimo kaina)
* Keityklos, kuri tą kriptovaliutą siūlo brangiausiai, pavadinimas
* Kaina USD už vnt. (pardavimo kaina)
* Pelnas procentais.


Bonus: Leiskite vartotojui pasirinkti, iš kiek valiutų jis nori lentelės (iki 100)

Į ką atkreipti dėmesį:

* Iš valiutų TOP10 reikia išmesti USDT(Tether). Tai dolerio ekvivalentas kriptovaliutose. Mūsų nedomina USD/USDT prekyba.
* Iš keityklų išmeskite 'BCex', ji meta nesąmoningas reikšmes (x10). Jeigu dar pastebėsite panašių - meskit lauk.
* Tai tik teorinis modelis, realybėje procesas kur kas sudėtingesnis, nesugalvokite taikyti praktikoje :)

Rezultatas turi atrodyti maždaug taip:

![](https://github.com/robotautas/kursas/blob/master/konsultacijos/0207/MDs/arbitrage.png)

# [Atsakymas](https://github.com/robotautas/kursas/tree/master/konsultacijos/0207/Code)

**Update(2020-02-19):** API laikinai, o gal ir ne laikinai nustojo reaguoti į tam tikrų monetų ID bandant ištraukti pasiūlymus iš keityklų. Response grąžina None, ir tai sugadina žodyno struktūrtą. Išspręsti rekomenduočiau naudojant try/except blokus arba if/else. Arba perdarant struktūrą į json friendly, nurodant, kad nepavyko gauti duomenų.