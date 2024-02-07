Regular expression arba *regex* yra simbolių seka, kurios pagalba kuriame paieškos tekste šablonus. 
Ši technika nėra išskirtinai susijusi su Python ar kuria kita kalba. Tuo pačiu tai yra greičiausias būdas sutikrinti, 
ar suvesta informacija atitinka standartus (pvz. email), surasti kažkokias atkarpas tekste ir pan pobūdžio 
užduotims vykdyti.

www.pythex.org - svetainė, kurioje galima praktikuotis, tikrinti savo regex šablonus. Pvz. įvedus vieną raidę a, regex
išgaudo visas raides tikrinamame tekste.

![a](https://github.com/robotautas/kursas/blob/master/RegEx/01a.png)

įvedus žodį rodo, surandami visi žodžiai 'rodo':

![rodo](https://github.com/robotautas/kursas/blob/master/RegEx/02rodo.png)

regex'as turi savo sintaksę, kurios pagalba galime apsibrėžti pačias įvairiausias paieškos tekste užklausas.

* \d	skaičius
* \D	neskaičius
* \s	tuščias tarpas (whitespace) [ \t\n\r\f\v] (space, tab, newline, ir pan.)
* \S	ne tuščias tarpas - viskas, kas ne tarpas.
* \w	alphanumeric: [0-9a-zA-Z_] - skaičiai nuo 0 iki 9, didžiosios ir mažosios raidės A-Z, simbolis '_'.
UTF simboliai nėra alphanumeric.
* \W	viskas, kas nėra prieš tai išvardintame punkte. 
* .     bet koks simbolis išskyrus eilutėspabaigos simbolį

pabandykime tiesiog įvesti \w:

![\w](https://github.com/robotautas/kursas/blob/master/RegEx/03%5Cw.png)

Rezultate matome, kad išrinktos visos alphanumeric reikšmės. 
Deja, UTF-8 simboliai nepakliūna į šią kategoriją, todėl lietuviškos raidės neišgaudytos. 
Vėliau aptarsime, kaip šitą problemą apeiti. Tarpus galime išrankioti su \s, skaičius su \d. 
Jeigu norime išgaudyti ir tarpus ir skaičius, naudojame loginį 'arba' simbolį '|':

![\s|\d](https://github.com/robotautas/kursas/blob/master/RegEx/04%5Cs%7C%5Cd.png)

svarbi regex sintaksės dalis yra vadinami Quantifiers. Jų pagalba šablone nustatome, kiek 
kartų simbolis atsikartoja šablone:

* \+    Vieną ar daugiau kartų
* {x}   Lygiai x kartų
* {x,y} Nuo x iki y kartų
* {x,}  x arba daugiau kartų
* \*    Nulį ar daugiau kartų
* ?     kartą, arba nei karto (optional)


Tarkime, iš duoto teksto norime ištraukti '(2017 m.)':

![](https://github.com/robotautas/kursas/blob/master/RegEx/05.png)

* Panagrinėkime - \( ištraukia skliaustelį, kadangi skliaustelis regex'o sintaksėje turi paskirtį, 
prieš jį naudojame *escape* simbolį '\\'.
* Toliau turim \d+. Reiškia skaičius gali atsikartoti vieną ir daugiau kartų.
* Paskui eina tarpas - \s.
* raidei m pagauti panaudojome \w.
* '.)'  kombinacija yra du NE alphanumerical simboliai, tiesiog panaudojome \W{2}

Turėkite omenyje, kad nėra vieno varianto šiai užduočiai atlikti, galime naudoti, pvz. \W\d{4}\s?m\W{1,2}. Arba 
tiesiog \\(2017 m\\.\\). Viskas priklauso nuo to ar ieškome daugiau šablono *(pattern)*, ar konkrečios atkarpos.


Arba, tarkime mums prireikė visų keturženklių skaičių. Atkreipkite dėmesį, metai užrašomi be tarpo, pvz. 2017, o kiti 
keturženkliai su pvz. 1 034.

![\d\s?\d{3}](https://github.com/robotautas/kursas/blob/master/RegEx/06%5Cd%5Cs%3F%5Cd%7B3%7D.png)

Laužtiniai skliaustai naudojami simbolių, kurie priklauso juose nurodytai grupei, paieškai. Tarkime [A-Za-z0-9] 
išrinks didžiąsias raides, mažąsias raides ir skaičius nuo 0 iki 9. [ąčęėįšųūž] išrankios lietuviškas raides, o, pvz, 
[\wąčęėįšųūž]+ išrinks visus žodžius ir skaičius lietuviškame tekste. (iš tiesų, Python'e paprasčiau su unicode simboliais, 
o šiame puslapyje geriau su angliškais tekstais praktikuotis).

![](https://github.com/robotautas/kursas/blob/master/RegEx/07skliaustai.png)

Dar šiek tiek sintaksės:
* ^ - ieško šablono tik iš eilutės pradžios *(\* Naudojamas laužtiniuose skliaustuose turi reikšmę NOT)*
* $ - ieško šablono tik iš eilutės pabaigos
* \b - žodžio ribos simbolis

Pvz.:

![](https://github.com/robotautas/kursas/blob/master/RegEx/08d4.png)

Šiuo atveju mūsų regex'as pasigauna abudu keturženklius. Jeigu mes norėtumėm, kad pasigautų tik pirmąjį, 
kuris nesiriboja su kitais simboliais, prieš ir po naudotumėm \b:

![](https://github.com/robotautas/kursas/blob/master/RegEx/09.png)

Jeigu mums prireiktų atkarpos 'blablabla', tai tiesiog suvedus tai į šabloną, mums išrinks visas blablabla. 
Tačiau, prireikus tokios, kuri nesiriboja su jokiais kitais žodžiais, reikia daryti taip:

![](https://github.com/robotautas/kursas/blob/master/RegEx/10blablabla.png)

Jeigu mus domina žodis, kuriuo prasideda eilutė, rašome taip:


![](https://github.com/robotautas/kursas/blob/master/RegEx/11%5Eblablabla.png)

O simbolių kombinacijas eilutės pabaigoje išrenkame taip:

![](https://github.com/robotautas/kursas/blob/master/RegEx/11blablabla%24.png)

Paskutinė sintaksės porcija:

* | - loginis 'arba'
* () - grupavimas


Pvz.:

![](https://github.com/robotautas/kursas/blob/master/RegEx/12mrmrs.png)

Panagrinėkime šabloną (Mr.|Mrs.)\s([A-Z\w]+\s[A-Z\w]+):
* (Mr.|Mrs.) - ieško Mr. ARBA Mrs. Vienas iš dviejų.
* \s - tarpas
* ([A-Z]\w+\s[A-Z]\w+) - Ieško dviejų žodžių, prasidedančių didžiąja raide, atskirtų vienu tarpu.

paveikslėlyje atkreipkite dėmesį į *Match Captures* skiltį. Matome, kad rezultatas išskirstytas į grupes, 
t.y. 1. kreipinys 2. Vardas Pavardė, nes jos išskirtos skliausteliuose. Programuojant Python aplinkoje galėsime
skirstyti užklausos rezultatus pagal grupes.

# Užduotys

http://pythex.org įkelkite tekstą:

Buveinės adresas: Konstitucijos pr. 20A, 03502 Vilnius

Telefonai:

1884 arba +370 5 268 4444 (Privatiems klientams)

1633 arba +370 5 268 4422 (Verslo klientams)

Faksas: (8 5) 258 2700

El. paštas: info@swedbank.lt

Įmonės kodas: 112029651

PVM mokėtojo kodas: LT120296515

Banko sąskaita: LT55 7300 0100 0000 0036

Banko kodas: 73000

SWIFT kodas: HABALT22

* Išrinkite visus žodžius, prasidedančius viena didžiąja raide.
* Išrinkite visus žodžius, kurie yra iš visų didžiųjų raidžių (PVM, SWIFT, HABALT22)
* Parašykite šabloną trumpąjam telefono numeriui (nereikia idealaus, tiesiog išrinkite 1884 ir 1663)
* Parašykite šabloną ilgąjam telefono numeriui
* Parašykite šabloną fakso numeriui
* Parašykite šabloną, kuris tiktų ir ilgąjam telefono numeriui, ir faksui (naudokite '|' ir grupavimą)
* Parašykite šabloną banko sąskaitos numeriui
* Parašykite šabloną PVM mokėtojo kodui
* Išrinkite visus žodžius prieš dvitaškį
* Parašykite paprastą šabloną el. paštui

[a-zA-Z0-9._%-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,6} - Tai yra nesudėtingas el. pašto šablonas. Išnagrinėkite, palyginkite su savo sukurtu.
Nebūtina kas kartą kurti to, kas jau senai atitirbta. Internete gausu informacijos apie dažniausiai naudojamus regex šablonus. Pvz. https://digitalfortress.tech/tricks/top-15-commonly-used-regex/ - pasinagrinėkite.

