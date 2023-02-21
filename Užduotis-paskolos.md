# 1 etapas
## Sukurti programą, kuri:
* Leistų vartotojui įvesti norimos paskolos sumą, palūkanas, terminą
* Užklausus atspausdintų įvestos norimos paskolos duomenis, bendrą palūkanų sumą bei bendrą gražintiną sumą
* Užklausus atspausdintų detalų paskutinės paskolos mokėjimo grafiką (lentelę)
## Galima vartotojo meniu struktūra:
1. Įvesti paskolos duomenis
2. Parodyti paskolos informaciją
3. Parodyti paskolos mokėjimo grafiką
4. Baigti darbą
## Galima programos struktūra:
* Klasė main, kurioje yra viso bendravimo su vartotoju logika
* Klasė Paskola su savybėmis suma, terminas, palūkanos
* Joje yra metodas paskolos_informacija(), kuris parodo paskolos informaciją (suma, terminas, palūkanos), mokėtinų palūkanų sumą bei bendrą mokėtiną sumą
* Joje yra metodas mokejimo_grafikas(), kuris parodo visą mokėjimo grafiko informaciją (lentelę)
## Paskolos mokėjimo grafiko skaičiavimo logika:
* Iš vartotojo pasiimame: sumą, terminą ir palūkanų normą (procentais)
* Gražintina stabili mėnesio suma paskaičiuojama bendrą paskolos sumą padalinus iš termino (mėnesių).
* Mėnesio likutis paskaičiuojamas iš mėnesio gražintinos sumos atimant gražintiną to mėnesio sumos dalį.
* Mėnesio palūkanos paskaičiuojamos pagal tokią formulę: (mėnesio likutis * palūkanos) / 12 (nes nurodomos metinės palūkanos)
* Mėnesio bendra mokėtina suma paskaičiuojama prie gražintinos mėnesio sumos pridėjus priskaičiuotas palūkanas
Linijinio mokėjimo grafiko pavyzdys:
https://github.com/DonatasNoreika/Python-pamokos/blob/master/paskolos_grafiko_pavyzdys.jpg

# 2 etapas
* Padaryti meniu punktą, kurį pasirinkus, parodytų visų prieš tai įvestų užklausų informaciją (papildomai galima padaryti, kad jas galima būtų koreguoti, atspausdinti pasirinktos paskolos išsamią informaciją bei mokėjimo grafiką)
* Padaryti, kad kiekvieną kartą paskaičiuojant paskolos mokėjimo grafiką, jis būtų išsaugomas .csv faile.
# 3 etapas
* Padaryti, kad išjungus programą, įvesti duomenys nedingtų (pickle?)
* Sukurti grafinę vartotojo sąsają su Flask
* Padaryti, kad Flask atvaizduotų visą mokėjimo grafiką (Pandas?)
* Padaryti, kad būtų atvaizduoti norimi grafikai apie paskolą (Matplotlib, Searborn)
# 4 etapas
Padaryti validaciją vartotojo įvedamiems duomenims. Pvz, vietoje sumos įvedus žodį, programa ne lūžtų, o paprašytų dar kartą įvesti duomenis teisingai. Galima panaudoti Regex, Try/Except, get/set metodus ir kt.

* Sukurti papildomą meniu punktą, kurį pasirinkus įvestos paskolos duomenys būtų išsiųsti vartotojo nurodytu el. pašto adresu.
* Sukurti programos logerį/logerius
