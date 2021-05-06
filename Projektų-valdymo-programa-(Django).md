Programa, skirta projektų valdymui. Leidžia įvesti projektus, jiems priskirtus darbus, klientą, vadovą, darbuotojus, sąskaitas.

Labai panaši, [kaip darėme su Odoo](https://github.com/DonatasNoreika/projektai/wiki/Kurso-programa:-projekt%C5%B3-valdymas).

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
