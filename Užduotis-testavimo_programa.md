Tikslas: sukurti egzaminavimo programą, kuri vartotojui pateiktų klausimus, leistų pasirinkti atsakymus, išsprendus testą parodytų rezultatą.

# 1 etapas - DB projektavimas ir sukūrimas
Suprojektuoti duomenų bazę (nupaišant diagramą) ir sukurti sqlite duomenų bazę, kuri:
* Saugotų testo klausimus, atsakymus, informaciją, kuris atsakymas teisingas.
* Pageidautina, kad saugotų kiekvieno sprendimo datą ir rezultatą.
* Pageidautina, kad būtų saugoma kelių vartotojų informacija
* Pageidautina, kad klausimas galėtų turėti neribotą kiekį atsakymų
* Pageidautina, kad po klausimu galima būtų pažymėti kelis teisingus atsakymus
* Pageidautina, būtų saugoma detali kiekvieno vartotojo sprendimo informacija (kiekvienas sprendimo klausimas ir pasirinktas atsakymas)
Pabandyti užpildyti sukurtą duomenų bazę duomenimis

Projektavimui galite naudoti https://app.sqldbm.com/

# 2 etapas - programos UI sukūrimas su SQLAlchemy
Padaryti programos UI su konsole, naudojant SQLAlchemy (be tiesioginių sql užklausų), kuri:
* Parodytų vartotojui testo klausimus su atsakymais.
* Leistų pasirinkti atsakymą (-us), išsprendus testą parodytų rezultatą (kiek iš kiek klausimų yra teisingi).
* Leistų sukurti vartotojus ir juos pasirinkti.
* Išsaugotų kiekvieno sprendimo informaciją: datą, rezultatą.
* Išsaugotų kiekvieną atsakytą klausimą ir pasirinktą atsakymą (-us), kad vėliau juos galima būtų peržiūrėti.
* Leistų įvesti naujus testus su klausimais ir atsakymais.

Jei jūsų 1 etape sukurta duomenų bazė neleidžia padaryti kažkurių iš aprašytų funkcijų, darykite programą pagal savo suprojektuotą duomenų bazę.
