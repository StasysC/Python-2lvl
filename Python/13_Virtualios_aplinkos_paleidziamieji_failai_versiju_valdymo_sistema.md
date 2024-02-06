# Virtualios aplinkos (VENV)
## Kaip pažiūrėti, kokie paketai (moduliai) įdiegti sistemoje ?
Windows komandinėje eilutėje (Win + c, m, d + Enter):

C:\Users\Vartotojas>pip list
```
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
(venv) C:\Users\Donoras\Desktop\Projektas>pip list –local
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
```
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
