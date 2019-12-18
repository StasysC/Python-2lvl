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

04\s|\d

svarbi regex sintaksės dalis yra vadinami Quantifiers. Jų pagalba šablone nustatome, kiek 
kartų simbolis atsikartoja šablone:

* \+    Vieną ar daugiau kartų
* {x}   Lygiai x kartų
* {x,y} Nuo x iki y kartų
* {x,}  x arba daugiau kartų
* \*    Nulį ar daugiau kartų
* ?     kartą, arba nei karto (optional)


Tarkime, iš duoto teksto norime ištraukti '(2017 m.)':

05\(\d+\s\w\W{2}

* Panagrinėkime - \( ištraukia skliaustelį, kadangi skliaustelis regex'o sintaksėje turi paskirtį, 
prieš jį naudojame *escape* simbolį '\\'.
* Toliau turim \d+. Reiškia skaičius gali atsikartoti vieną ir daugiau kartų.
* Paskui eina tarpas - \s.
* raidei m pagauti panaudojome \w.
* '.)'  kombinacija yra du NE alphanumerical simboliai, tiesiog panaudojome \W{2}

Turėkite omenyje, kad nėra vieno varianto šiai užduočiai atlikti, galime naudoti, pvz. \W\d{4}\s?m\W{1,2}. Arba 
tiesiog \(2017 m\.\). Viskas priklauso nuo to ar ieškome daugiau šablono *(pattern)*, ar konkrečios atkarpos.


Arba, tarkime mums prireikė visų keturženklių skaičių. Atkreipkite dėmesį, metai užrašomi be tarpo, pvz. 2017, o kiti 
keturženkliai su pvz. 1 034.

06\d\s?\d{3} 




