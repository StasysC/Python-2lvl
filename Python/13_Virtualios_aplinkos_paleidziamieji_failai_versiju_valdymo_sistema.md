# Virtualios aplinkos (VENV)
## Kaip pažiūrėti, kokie paketai (moduliai) įdiegti sistemoje ?
Windows komandinėje eilutėje (Win + c, m, d + Enter):
```
C:\Users\Vartotojas>pip list

Package Version
-------------- --------
decorator 4.0.10
docutils 0.12
pefile 2018.8.8
pip 18.1
PyInstaller 3.4
pytz 2016.7
pywin32-ctypes 0.2.0
setuptools 40.6.2
```
## Kaip sukurti virtualią programavimo aplinką?
```
C:\Users\Vartotojas>cd Desktop

C:\Users\Vartotojas\Desktop>mkdir Projektas

C:\Users\Vartotojas\Desktop>cd Projektas

C:\Users\Vartotojas\Desktop\Projektas>python -m venv venv
```
## Kaip aktyvuoti/deaktyvuoti virtualią programavimo aplinką?
```
C:\Users\Donoras\Desktop\Projektas>venv\Scripts\activate.bat
(venv) C:\Users\Donoras\Desktop\Projektas>pip list

Package Version
---------- -------
pip 18.1
setuptools 40.6.2

(venv) C:\Users\Donoras\Desktop\Projektas>python sveiki.py
(venv) C:\Users\Donoras\Desktop\Projektas>deactivate
```
## Kaip įdiegti paketus į virtualią programavimo aplinką?
```
(venv) C:\Users\Donoras\Desktop\Projektas>pip install pyinstaller
(venv) C:\Users\Donoras\Desktop\Projektas>pip list

Package Version
-------------- ---------
altgraph 0.16.1
future 0.17.1
macholib 1.11
pefile 2019.4.18
pip 18.1
PyInstaller 3.4
pywin32-ctypes 0.2.0
setuptools 40.6.2
```
## Kaip sukurti reikalavimų failą?
```
(venv) C:\Users\Donoras\Desktop\Projektas>pip freeze

altgraph==0.16.1
future==0.17.1
macholib==1.11
pefile==2019.4.18
PyInstaller==3.4
pywin32-ctypes==0.2.0
```
## Tai išsaugome į failą requirements.txt:
```
(venv) C:\Users\Donoras\Desktop\Projektas>pip freeze > requirements.txt
```
## Kaip įdiegti paketus iš reikalavimų failo?
Naujoje virtualioje aplinkoje (ištrinus venv katalogą):
```
(venv) C:\Users\Donoras\Desktop\Projektas>pip install -r requirements.txt

(venv) C:\Users\Donoras\Desktop\Projektas>pip list

Package Version
-------------- ---------
altgraph 0.16.1
future 0.17.1
macholib 1.11
pefile 2019.4.18
pip 18.1
PyInstaller 3.4
pywin32-ctypes 0.2.0
setuptools 40.6.2
```
## Pastabos
* Į virtualią aplinką nededame jokių projekto (.py ir kitų) failų
* Virtualios aplinkos katalogo nededame į versijų valdymo sistemų repozitorijas
* Bet dedame requirements failą, kad kiti kodu besinaudojantys asmenys galėtų susikurti savo virtualias aplinkas

## Kaip sukurti virtualią aplinką su paketais iš sistemos aplinkos?
Naujoje virtualioje aplinkoje:
```
C:\Users\Donoras\Desktop\Projektas>python -m venv venv --system-site-packages

C:\Users\Donoras\Desktop\Projektas>venv\Scripts\activate.bat

(venv) C:\Users\Donoras\Desktop\Projektas>pip list

Package Version
-------------- --------
altgraph 0.16.1
Babel 2.3.4
decorator 4.0.10
docutils 0.12
future 0.17.1
macholib 1.11
pefile 2018.8.8
pip 18.1
PyInstaller 3.4
pytz 2016.7
pywin32-ctypes 0.2.0
setuptools 40.6.2
```
```
(venv) C:\Users\Donoras\Desktop\Projektas>pip install SQLAlchemy

(venv) C:\Users\Donoras\Desktop\Projektas>pip list
Package Version
-------------- --------
altgraph 0.16.1
Babel 2.3.4
decorator 4.0.10
docutils 0.12
future 0.17.1
macholib 1.11
pefile 2018.8.8
pip 18.1
PyInstaller 3.4
pytz 2016.7
pywin32-ctypes 0.2.0
setuptools 40.6.2
SQLAlchemy 1.3.3
```
```
(venv) C:\Users\Donoras\Desktop\Projektas>pip list –-local
Package Version
---------- -------
pip 18.1
setuptools 40.6.2
SQLAlchemy 1.3.3
```
```
(venv) C:\Users\Donoras\Desktop\Projektas>deactivate
C:\Users\Donoras\Desktop\Projektas>pip list

Package Version
-------------- --------
altgraph 0.16.1
Babel 2.3.4
decorator 4.0.10
docutils 0.12
future 0.17.1
macholib 1.11
pefile 2018.8.8
pip 18.1
PyInstaller 3.4
pytz 2016.7
pywin32-ctypes 0.2.0
setuptools 40.6.2
```
# EXE failų kūrimas

## Pyinstaller diegimas Windows sistemoje
Diegimas Windows komandinėje eilutėje cmd (Win, c, m, d, ENTER):

```
C:\Users\Donoras\Desktop\Projektas>pip install pyinstaller
```
## Padarome EXE failą iš programos su konsole
```python
print("Sveikas, pasauli!")
```
## Atidarome cmd arba PyCharm terminalą:
Paleidžiame terminale:
```
pyinstaller --onefile sveiki.py
```
Problema: dukart spragtelėjus, langas iškart užsidaro

Sprendimas:
```python
print("Sveikas, pasauli!")
input("Norėdami uždaryti spauskite ENTER")
```
## Padarome EXE failą iš programos su grafine sąsaja
```python
from tkinter import *

pagrindinis = Tk()
uzrasas = Label(pagrindinis, text="Sveikas, pasauli!")
uzrasas.pack()
pagrindinis.mainloop()
```
Paleidžiame terminale:
```
pyinstaller --onefile -w sveiki2.py
```
## Kaip pakeisti lango ikoną, pavadinimą, lango dydį

Kaip gauti norimą ikoną (PNG, 32px): www.flaticon.com

Kaip konvertuoti ikoną į norimą formatą: https://icoconvert.com/
```python
from tkinter import *

pagrindinis = Tk()
uzrasas = Label(pagrindinis, width=40, height=10, text="Sveikas, pasauli!")
pagrindinis.title("Mano programa")
pagrindinis.iconbitmap(r'sveikinimasis.ico')
uzrasas.pack()
pagrindinis.mainloop()
```
Paleidžiame terminale:
```
pyinstaller --onefile -w sveikinimas.py
```
Kaip pakeisti programos ikoną

Paleidžiame terminale:
```
pyinstaller --onefile -w --icon=sveikinimas.ico sveikinimas.py
```
# Versijų valdymo sistema (GIT)
## Kas tai yra?
Versijų valdymo sistemos (angl. Version Control System arba VCS) seka bendrų projektų, kuriamų grupės žmonių, pokyčių istoriją

Naudosime vieną populiariausių versijų valdymo sistemą GIT – www.github.com (dar yra GitLab, Bitbucket)

## Ką leidžia VCS (GIT)?
* Saugoti visus kodo pakeitimus ir nesunkiai gražinti kodą į norimą, prieš tai buvusią padėtį
* Su tuo pačiu kodu lygiagrečiai dirbti (keisti) daugeliui žmonių
* Lengvai dalintis, rodyti, leisti peržiūrėti kolegoms parašytą kodą per specialią svetainę (pvz. www.github.com)
* Nuolat išsaugoti paskutinius pakeitimus ne tik lokaliai, bet ir serveryje
* Lengviau pateikti kodą į produkciją (pvz., publikuoti sukurtą svetainę internete, skelbti pakeitimus)

## Kaip įdiegti GIT Windows sistemoje?
* Užsiregistruoti svetainėje www.github.com.
* Įdiegti GIT programą iš https://git-scm.com/downloads (diegiant visuomet spausti „Next“).
* Patikrinti ar veikia, Windows konsolėje (Win + c, m, d + Enter) įrašius „git“ (jei išmeta pagalbos informaciją apie git, reiškia veikia).

## Kaip nustatyti GIT?
Windows konsolėje (Win + c, m, d + Enter):

1. Nustatyti vardą:
```
git config --global user.name "Vardas Pavarde"
```
2. Nustatyti el. pašto adresą:
```
git config --global user.email el@pastas.com
```
3. Patikrinti ar pasikeitė:
```
git config --list
```
## Kaip susieti kompiuterį su GitHub (per SSH raktą)?
1. Atidaryti programą Git Bash (Win + g, i, t, , b, a, s, h + Enter).

2. Sugeneruoti SSH raktą paleidus šią komandą:
```
ssh-keygen -t rsa -b 4096 -C "el@pastas.com"
```
(galima visas užklausas patvirtinti nieko nevedant, tik spaudžiant Enter).

3. Su bet kokiu teksto redaktoriumi atidaryti sugeneruotą rakto failą id_rsa.pub, pažymėti kodą komanda CTRL+C.

4. Svetainėje www.github.com spausti ant vartotojo ikonos viršutiniame dešiniajame kampe, pasirinkti Settings, tuomet SSH and GPG keys. Tada spausti mygtuką New SSH key.

5. Laukelyje Title įrašyti norimą pavadinimą, pvz. Namų kompiuteris, pele pažymėti lauką key ir paspausti CTRL+V (bus įklijuotas 3 žingsnyje nukopijuotas SSH kodas), galiausiai spausti Add SSH Key.

## Kaip sukurti tuščią GitHub projektą (repozitoriją)?
1. Pagrindiniame www.github.com puslapyje (prisijungę savo vardu ir slaptažodžiu) spauskite Start a project.

2. Laukelyje Repository name įrašykite norimą projekto pavadinimą (be tarpų) ir spauskite mygtuką Create repository. Atsidariusiame lange pamatysite komandas, reikalingas pridėti failus į repozitoriją

## Kaip pridėti failą į Git repozitoriją?
1. Atidarykite Windows konsolę (Win + c, m, d + Enter), atidarykite vietą, kur kursite projekto failus (norėdami dirbti Windows darbastalyje, konsolėje įveskite cd Desktop ir spauskite Enter).

2. Norimoje vietoje sukurkite naują failą, pavyzdžiui, suvesdami komandą:
```
echo "# test" >> README.md
```
3. Sustatykite šią vietą, kaip stebimą su GIT, įvesdami komandą:
```
git init
```
4. Pridėkite į repozitoriją sukurtą failą, paleisdami komandą:
```
git add README.md
```
arba:
```
git add .
```
5. Patikrinkite, ar failas buvo pridėtas, paleisdami komandą:
```
git status
```
6. Užfiksuokite pakeitimus, paleisdami komandą:
```
git commit -m "pirmas commit"
```
## Kaip išsaugoti pakeitimus į www.github.com?
1. Nustatyti nuotolinės repozitorijos, į kurią bus keliami pakeitimai, kelią, pvz.:
```
git remote add origin git@github.com:StasysC/Python-2lvl.git
```
(kelią rasite užėję į norimą projektą www.github.com svetainėje).

2. Užfiksuokite pakeitimus, paleidę komandą:
```
git push -u origin main
```
(į klausimą are you sure you want to continue connecting (yes/no)?, atsakykite įvesdami yes ir spausdami Enter)

## Kaip pridėti dar vieną failą į GIT repozitoriją?
1. Projekto kataloge sukurkite naują failą, pvz. paleisdami komandą:
```
echo "# naujas" >> failas2.txt
```
2. Pridėkite į repozitoriją sukurtą failą, paleisdami komandą:
```
git add failas.txt
```
arba:
```
git add .
```
3. Užfiksuokite pakeitimus, paleisdami komandą:
```
git commit -m "pridetas antras failas"
```
4. Užfiksuokite pakeitimus į GitHub, paleidę komandą:
```
git push -u origin main.
```
Padarę vieno iš repozitorijos failo pakeitimą ir pakartoję 2-4 žingsnius, galite taip pat užfiksuoti šiuos pakeitimus į GitHub.

## Kaip panaikinti paskutinius pakeitimus?
1. Paredaguokite norimą failą, pvz. failas2.txt. Įvedę šią komandą matysite, kuriame faile buvo atlikti pakeitimai:
```
git status
```
2. Atšaukite paskutinius pakeitimus, įvedę komandą:
```
git reset failas2.txt
```
3. Patikrinkite, ar pakeitimai buvo atlikti, įvedę:
```
git status
```
## Kaip sukurti GitHub repozitorijos kopiją kompiuteryje?
1. Atidarykite Windows konsolę (Win + c, m, d + Enter), atidarykite vietą, kur kursite projekto failus (norėdami dirbti Windows darbastalyje, konsolėje įveskite cd Desktop ir spauskite Enter).

2. Padarykite nutolusios repozitorijos kopiją, paleisdami komandą:
```
git clone git@github.com:DonatasNoreika/test.git
```
(norimos repozitorijos adresą galite rasti nuėję į jos puslapį www.github.com ir paspaudę mygtuką Clone or download).

# Užduotys
## 1 užduotis
Išbandyti šioje pamokoje aprašytus žingsnius:

* Sukurti naują projektą su .py failu
* Jame sukurti virtualią aplinką
* Ją aktyvuoti
* Į ją įdiegti, pavyzdžiui, pyinstaller paketą
* Susikurti iš virtualios aplinkos requirements.txt failą

## 2 Užduotis 
Sukurti paleidžiamąjį failą iš programos, kuri:

* Leistų vartotojui įvesti metus nuo ir metus iki
* Atspausdintų visus keliamuosius metus pagal duotą rėžį
* Paleidžiamasis failas turi turėti norimą ikoną


## 3 Užduotis 
* Padaryti paleidžiamąjį failą iš 11 paskaitos 4 programos (pilna programa su vartotojo sąsaja)
* Programa turi turėti programos lango ikoną ir norimą pavadinimą
* Paleidžiamasis failas turi turėti norimą ikoną
