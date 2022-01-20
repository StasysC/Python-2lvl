Klasė: Tankas

Metodai: pirmyn, atgal, kairėn, dešinėn, šūvis, info, ...

Kintamieji turi:
* saugoti tanko koordinates,
* saugoti tanko kryptį,
* saugoti šūvių skaičių į kiekvieną kryptį.

* Tankas gali judėti pirmyn (į Šiaurę), dešinėn (į Rytus), atgal (į
Pietus), kairėn (į Vakarus) per vieną poziciją. Pvz. „tankas pajuda
kairėn“, tai reiškia jis pasisuko 90 laipsnių ir pajudėjo per vieną
vienetą į Vakarus.
* Tankas gali šaudyti tik ta kryptimi, į kurią jis yra pasisukęs.

Metodas info() turi parodyti:
* į kurią kryptį tankas šiuo metu yra pasisukęs,
* kokios yra jo koordinatės,
* kiek iš viso atliko šūvių
* kiek atliko šūvių į kiekvieną kryptį atskirai.

Visas tanko ir informacijos valdymas turi būti atliktas konsolėje
(grafinio interfeiso nereikia). Tam reikės sukurti meniu ir priimti
vartotojo nurodymus. Veiksmai turi būti atliekami (kviečiami metodai)
tol, kol vartotojas nesustabdys programos (pavyzdžiui, pasirinkęs tam
tikrą meniu punktą).

![Tanko iliustracija](https://github.com/robotautas/kursas/blob/master/tanko%20iliustracija.png)

## 2 etapas

Patobulinkite programą taip, kad koordinačių sistemoje būtų generuojamas taikinys. Tanko užduotis - atsidurti tinkamoje pozicijoje ir reikiama kryptimi, kad iššovus būtų fiksuojamas pataikymas. Tankui pataikius, konsolėje matome užrašą "pataikei" ir tuoj pat sugeneruojamas naujas taikinys. 
## 3 etapas

Sugalvokite taškų sistemą, pvz už pataikymus galima skirti 100 taškų, už kiekvieną kitą veiksmą nubraukti 10 taškų. Sumuoti pataikymus. Pasibaigus taškams programa parodo, kiek numušta taikinių, ir pasibaigia. Galbūt galima saugoti high scores - pasibaigus įvedamas vardas ir žaidėjas su numuštų taikinių skaičiumi įrašomas į topus. Topus galbūt galima pažiūrėti su komanda 'top'. Sugalvokite kokių nors savo patobulinimų, sėkmės :)
