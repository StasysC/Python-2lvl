# ML praktikoje, užduotis.

Sukurkite Flask'o web-programėlę, kurioje į laukelius suvedę gėlės išmatavimus, gautumėm mašininio mokymosi modelio prognozę, t.y. gėlės porūšis ir nuotrauka. Kad nebūtų suvedami bet kokie duomenys, padarykite regex filtrą, prieš juos pateikiant modeliui. Galima darbo eiga:

* Pasidarykite virtualią aplinką, kurioje bus Flask, Seaborn, sklearn, numpy, pandas bibliotekos. 
* apmokykite modelį taip kaip jis buvo apmokytas paskaitoje, tik darykite tai .py faile. Tą modelį išsaugokite į pickle.
* tame pat faile sukurkite funkciją, kuri priimtų gėlės išmatavimus ir grąžintų prognozę.
* Sukurkite Flask programėlę, kuri generuos puslapį, kuriame bus forma į kurią bus suvedami gėlių išmatavimai.
* Išgaudykite tuos suvedamus duomenis, praleiskite per regex filtrą, ir atiduokite ML funkcijai, iš kurios pasiėmę rezultatus, siųskite į template. 
* programos - demonstracija ![](https://github.com/robotautas/kursas/raw/master/Machine%20Learning/webapp_demo.mkv).

  

