Programa, skirta projektų valdymui. Leidžia įvesti projektus, jiems priskirtus darbus, klientą, vadovą, darbuotojus, sąskaitas.

# Objektai:
## Projektas
- Pavadinimas
- Pradžios data
- Pabaigos data
- Klientas (ryšys su Klientas)
- Atsakingasis/vadovas (ryšys su User)
- Darbuotojai (ryšys su Darbuotojas)
- Darbai (ryšys su Darbas)
- Sąskaitos (ryšys su Sąskaita)
## Klientas
- Vardas
- Pavardė
- Įmonė
- Kontaktai (galima išskirstyti į atskirus laukus)
## Darbuotojas
- Vardas
- Pavardė
- Pareigos
## Darbas
- Pavadinimas
- Pastabos
## Sąskaita
- Išrašymo data
- Suma (galima pasudėtinginti, įterpiant sąskaitos eilutes)
# Užduotys:
1. Sukurti modelius pagal duotą aprašą.
2. Sukurti atitinkamus meniu administravimo svetainėje (įtraukiant norimus filtrus, paieškos laukus, nustatymus ir t.t.).
3. Padaryti projektų atvaizdavimo puslapį (ne administravimo puslapyje) su išsamia projektų informacija (pagrindiniai duomenys plius darbuotojai, darbai, sąskaitos).
4. Padaryti, kad prie svetainės būtų leidžiama prisiregistruoti ir prisijungti išoriniam vartotojui. Taip pat įgyvendinti slaptažodžio pakeitimą.
5. Padaryti, kad prisijungusiam vartotojui būtų rodomi jam priskirti projektai (tuos, už kuriuos jis yra atsakingasis).
6. Padaryti, kad projektų įrašai būtų puslapiuojami.
7. Leisti prie projekto prisegti nuotrauką (per admin puslapį). Atvaizduoti ją projektų sąraše ir išsamiame projekto aprašyme.
8. Prie projekto pridėti aprašymo lauką (per admin puslapį), kuriame galima būtų įrašyti ir atvaizduoti informaciją HTML formatu (tiny-mce biblioteka).
