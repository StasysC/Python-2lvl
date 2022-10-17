Programa, skirta projektų valdymui. Leidžia įvesti projektus, jiems priskirtus darbus, klientą, vadovą, darbuotojus, sąskaitas.

## Objektai:

### Projektas
* Pavadinimas
* Pradžios data
* Pabaigos data
* Klientas (ryšys su Klientas)
* Atsakingasis/vadovas (ryšys su User)
* Darbuotojai (ryšys su Darbuotojas)
* Darbai (ryšys su Darbas)
* Sąskaitos (ryšys su Sąskaita)


### Klientas
* Vardas
* Pavardė
* Įmonė
* Kontaktai (galima išskirstyti į atskirus laukus)


### Darbuotojas
* Vardas
* Pavardė
* Pareigos


### Darbas
* Pavadinimas
* Pastabos


### Sąskaita
* Išrašymo data
* Suma
(galima pasudėtinginti, įterpiant sąskaitos eilutes)


## 1 etapas:
1. Sukurti modelius pagal duotą aprašą.
2. Sukurti atitinkamus meniu administravimo svetainėje (įtraukiant norimus filtrus, paieškos laukus, nustatymus ir t.t.).
2. Padaryti projektų atvaizdavimo puslapį (ne administravimo puslapyje) su išsamia projektų informacija.

## 2 etapas:
1. Padaryti, kad prie svetainės būtų leidžiama prisiregistruoti ir prisijungti išoriniam vartotojui. Taip pat įgyvendinti slaptažodžio pakeitimą.
2. Padaryti, kad prisijungusiam vartotojui būtų rodomi jam priskirti projektai (tuos, už kuriuos jis yra atsakingasis).
3. Padaryti, kad prisijungusiam vartotojui būtų rodomas išsamus projekto aprašymas (pagrindiniai duomenys plius darbuotojai, darbai, sąskaitos)
4. Padaryti, kad projektų įrašai būtų puslapiuojami.
5. Leisti prie projekto prisegti nuotrauką (per admin). Atvaizduoti ją projektų sąraše ir išsamiame projekto aprašyme.
6. Prie projekto pridėti aprašymo lauką (per admin), kuriame galima būtų įrašyti ir atvaizduoti informaciją HTML formatu (tiny-mce biblioteka).