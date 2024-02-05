# Kaip sukurti grafinę vartotojo sąsają (su Tkinter)
## Minimali programa:
```python
from tkinter import Tk, Label

langas = Tk()
langas.geometry("250x200")
uzrasas = Label(langas, text="Tiesiog tekstas")
uzrasas.pack()
langas.mainloop()
```
## Grafinės sąsajos objektai:
* Label – užrašas (kortelė)
* Button – mygtukas
* Entry – laukelis
* Menu – meniu
* Frame – rėmelis
* Checkbutton – varnelė
* Listbox – sąrašas
* Scrollbar – sąrašo slinkimo juosta

## Grafinių objektų formavimas rėmeliuose (su pack funkcija):
```python
from tkinter import Tk, Frame, Button, BOTTOM, LEFT, Y

langas = Tk()
langas.geometry("250x200")
virsutinis = Frame(langas)
apatinis = Frame(langas)

mygtukas1 = Button(virsutinis, text="1 mygtukas")
mygtukas2 = Button(virsutinis, text="2 mygtukas")
mygtukas3 = Button(virsutinis, text="3 mygtukas")
mygtukas4 = Button(apatinis, text="4 mygtukas")

virsutinis.pack()
apatinis.pack(side=BOTTOM)
mygtukas1.pack(side=LEFT)
mygtukas2.pack(side=LEFT)
mygtukas3.pack(side=LEFT)
mygtukas4.pack(side=BOTTOM, fill=Y)

langas.mainloop()
```
## Grafinių objektų formavimas lentelėje (su grid funkcija):
```python
from tkinter import *

langas = Tk()

uzrasas1 = Label(langas, text="Vardas")
laukas1 = Entry(langas)
uzrasas2 = Label(langas, text="Pavardė")
laukas2 = Entry(langas)
varnele = Checkbutton(langas, text="Pažymėk varnelę")

uzrasas1.grid(row=0, column=0, sticky=E)
laukas1.grid(row=0, column=1)
uzrasas2.grid(row=1, column=0, sticky=E)
laukas2.grid(row=1, column=1)
varnele.grid(row=2, columnspan=2)

langas.mainloop()
```
# Kaip įdėti funkciją paleidžiantį mygtuką:
```python
from tkinter import *
langas = Tk()

def spausdinti():
    print("Spausdina!")

mygtukas = Button(langas, text="Spausdinti", command=spausdinti)
mygtukas.pack()
langas.mainloop()

# Spausdina!
```
## Kaip esant skirtingiems vartotojo veiksmams, paleisti skirtingas funkcijas:
```python
from tkinter import *
langas = Tk()

def spausdinti(event):
    print("Paspaustas kairys pelės mygtukas!")

def spausdinti2(event):
    print("Paspaustas dešinys pelės mygtukas!")

def spausdinti3(event):
    print("Paspaustas ENTER!")

mygtukas = Button(langas, text="Spausdinti")
mygtukas.bind("<Button-1>", spausdinti)
mygtukas.bind("<Button-3>", spausdinti2)
langas.bind("<Return>", spausdinti3)
mygtukas.pack()

langas.mainloop()

# Paspaustas kairys pelės mygtukas!
# Paspaustas dešinys pelės mygtukas!
# Paspaustas ENTER!
```
Mygtukų kodus bind funkcijai rasite čia:

https://web.archive.org/web/20190515021108id_/http://infohost.nmt.edu/tcc/help/pubs/tkinter/web/key-names.html

https://docstore.mik.ua/orelly/other/python/0596001886_pythonian-chp-16-sect-9.html

Mygtukų kombinacijos:
```python
mygtukas.bind("<Control-Shift-Button-1>", spausdinti)
```
## Kaip per bind iškviesti funkciją be "event" argumento?
```python
from tkinter import *
langas = Tk()

def spausdinti():
    print("Spausdina!")

mygtukas = Button(langas, text="Spausdinti", command=spausdinti)
langas.bind("<Return>", lambda event: spausdinti())
mygtukas.pack()

langas.mainloop()
```
## Kaip per grafinę sąsają nuskaityti ir atspausdinti duomenis:
```python
from tkinter import *

langas = Tk()

def spausdinti():
    ivesta = laukas1.get()
    rezultatas["text"] = ivesta

uzrasas1 = Label(langas, text="Įrašykite žodį")
laukas1 = Entry(langas)
mygtukas = Button(langas, text="Įvesti", command=spausdinti)
rezultatas = Label(langas, text="")

uzrasas1.grid(row=0, column=0)
laukas1.grid(row=0, column=1)
mygtukas.grid(row=0, column=2)
rezultatas.grid(row=1, columnspan=3)

langas.mainloop()
```
## Kaip sukurti atvaizduojamą sąrašą:
```python
from tkinter import *

langas = Tk()
boksas = Listbox(langas)
sarasas = range(1, 200)
boksas.insert(END, *sarasas)
boksas.pack(side=LEFT)
langas.mainloop()
```
## Kaip pridėti sąrašo slinkimo juostą:
```python
from tkinter import *

langas = Tk()


sarasas = range(1, 200)

scrollbaras = Scrollbar(langas)
boksas = Listbox(langas, yscrollcommand=scrollbaras.set)
boksas.insert(END, *sarasas)
scrollbaras.config(command=boksas.yview)
boksas.pack(side=LEFT)
scrollbaras.pack(side=RIGHT, fill=Y)

langas.mainloop()

```
## Kaip pasiimti duomenis iš pažymėtos sąrašo vietos:
```python
from tkinter import *

langas = Tk()
sarasas = range(1, 200)

def spausdinti():
    pasirinkta = sarasas[boksas.curselection()[0]]
    uzrasas["text"] = pasirinkta

mygtukas = Button(langas, text="Spausdinti",
command=spausdinti)

uzrasas = Label(langas, text="Nieko")
boksas = Listbox(langas, selectmode=SINGLE)
boksas.insert(END, *sarasas)
boksas.pack(side=LEFT)
mygtukas.pack()
uzrasas.pack()
langas.mainloop()
```
## Kaip sukurti meniu:
```python
from tkinter import *
langas = Tk()

meniu = Menu(langas)
langas.config(menu=meniu)
submeniu = Menu(meniu, tearoff = 0)

meniu.add_cascade(label="Meniu", menu=submeniu)
submeniu.add_command(label="Pirmas")
submeniu.add_command(label="Antras")
langas.mainloop()
```
## Kaip meniu punktams priskirti funkcijas:
```python
from tkinter import *
langas = Tk()

meniu = Menu(langas)
langas.config(menu=meniu)
submeniu = Menu(meniu, tearoff = 0)

def antras():
    print("Antras!")

meniu.add_cascade(label="Meniu", menu=submeniu)
submeniu.add_command(label="Pirmas")
submeniu.add_command(label="Antras",
command=antras)
langas.mainloop()

# Antras!
```
## Kaip sukurti daugiau meniu, juos atskirti:
```python
from tkinter import *
langas = Tk()

meniu = Menu(langas)
langas.config(menu=meniu)
submeniu = Menu(meniu, tearoff = 0)
submeniu2 = Menu(meniu, tearoff = 0)
submeniu3 = Menu(meniu, tearoff = 0)

meniu.add_cascade(label="Meniu", menu=submeniu)
submeniu.add_command(label="Pirmas")

submeniu.add_command(label="Antras")
submeniu.add_separator()
submeniu.add_command(label="Trečias")

meniu.add_cascade(label="Meniu 2",
menu=submeniu2)
submeniu2.add_command(label="1")
submeniu2.add_command(label="2")

meniu.add_cascade(label="Meniu 3",
menu=submeniu3)

langas.mainloop()
```
## Statuso juostos (status bar) kūrimas:
```python
from tkinter import *
langas = Tk()

status = Label(langas, text="Nieko nedaro...", bd=1, relief=SUNKEN, anchor=W)
status.pack(side=BOTTOM, fill=X)
langas.mainloop()
```
Su mygtuku:
```python
from tkinter import *
langas = Tk()

def daryti():
    status["text"] = "Dabar daro"

mygtukas = Button(langas, text="Daryti", command=daryti)
status = Label(langas, text="Nieko nedaro...", bd=1, relief=SUNKEN, anchor=W)
status.pack(side=BOTTOM, fill=X)

mygtukas.pack()

langas.mainloop()
```
Jei statuso juosta formuojama lentelėje:
```python
status.grid(row=2, columnspan=3, sticky=W+E)
```
## Kaip sukurti veikiančią nuorodą:
```python
from tkinter import *
import webbrowser

def callback(url):
    webbrowser.open_new(url)

root = Tk()
link1 = Label(root, text="Google Hyperlink", fg="blue", cursor="hand2")
link1.pack()
link1.bind("<Button-1>", lambda e: callback("http://www.google.com"))

link2 = Label(root, text="Ecosia Hyperlink", fg="blue", cursor="hand2")
link2.pack()
link2.bind("<Button-1>", lambda e: callback("http://www.ecosia.org"))

root.mainloop()
```
## Kaip atidaryti nuotrauką:
```python
from tkinter import *
from PIL import ImageTk, Image

root = Tk()
img = ImageTk.PhotoImage(Image.open("paveiksliukas.JPG"))
panel = Label(root, image = img)
panel.pack(side = "bottom", fill = "both", expand = "yes")
root.mainloop()
```
## Kintamųjų naudojimas Tkinter programoje:
Jei kuriant programą su Tkinter, prireiks funkcijose panaudoti globalų kintamąjį, standartiniai kintamieji (pvz. kintamasis = "") nesuveiks. Todėl patartina naudoti StringVar, IntVar kintamuosius. Jie turi set() (reikšmės nustatymui) ir get() (kintamojo reikšmės gavimui) funkcijas. Atkreipkite dėmesį, kad jos gali būti kviečiamos tik funkcijose. Pvz:

StringVar panaudojimo pavyzdys:
```python
from tkinter import *

langas = Tk()

kintamasis = StringVar()
# kintamasis = ""

def funkcija():
    kintamasis.set("Naujas tekstas")
    print(kintamasis.get())
```
## Kaip tkinter programoje padaryti kelis langus:
```python
import tkinter as tk


class Demo1:
    def __init__(self, master):
        self.master = master
        self.frame = tk.Frame(self.master)
        self.button1 = tk.Button(self.frame, text='New Window', width=25, command=self.open_window)
        self.button1.pack()
        self.frame.pack()

    def open_window(self):
        self.new_window = tk.Toplevel(self.master)
        Demo2(self.new_window)


class Demo2:
    def __init__(self, master):
        self.master = master
        self.frame = tk.Frame(self.master)
        self.quitButton = tk.Button(self.frame, text='Quit', width=25, command=self.close_windows)
        self.quitButton.pack()
        self.frame.pack()

    def close_windows(self):
        self.master.destroy()


def main():
    root = tk.Tk()
    Demo1(root)
    root.mainloop()


if __name__ == '__main__':
    main()

```
# Užduotys
## 1 užduotis
Sukurti programą su grafine sąsaja, kuri:

* Turėtų laukelį su užrašu "Įveskite vardą", kuriame vartotojas galėtų įvesti vardą
* Turėtų mygtuką su užrašu "Patvirtinti", kurį nuspaudus, programa po lauku atspausdintų "Labas, {vardas}!"
  
![](https://github.com/StasysC/Python-2lvl/blob/master/Python/uzduotis1.jpg)

## 2 užduotis
Patobulinti 1 užduoties programą, kad ji:

* Atspausdintų pasisveikinimą ne tik nuspaudus mygtuką, bet ir paspaudus mygtuką "Enter"
## 3 užduotis
Patobulinti 2 užduoties programą, kad ji turėtų meniu pavadinimu "Meniu", kuriame:

* Būtų punktas "Išvalyti", kurį paspaudus išsitrintų tekstas eilutėje, kurioje spausdinamas pasisveikinimo tekstas
* Būtų punktas "Atkurti", kurį paspaudus pasisveikinimo teksto eilutėje butų atspausdintas paskutinis atspausdintas tekstas
* Būtų punktas "Išeiti", kurį paspaudus užsidarytų programos langas
* Tarp menių punktų "Atkurti" ir "Išeiti" būtų atskyrimo brūkšnys

![](https://github.com/StasysC/Python-2lvl/blob/master/Python/uzduotis3.jpg)

## 4 užduotis
Patobulinti 3 užduoties programą, kad ji turėtų statuso juostą apačioje, kurioje:

* Būtų rodoma "Sukurta", kai atspausdinamas pasisveikinimo tekstas
* Būtų rodoma "Išvalyta", kai ištrinamas pasisveikinimo tekstas
* Būtų rodoma "Atkurta", kai atkuriamas paskutinis pasisveikinimo tekstas
* Nuspaudus klaviatūros mygtuką "Escape", uždarytų programos langą
  
![](https://github.com/StasysC/Python-2lvl/blob/master/Python/uzduotis4.jpg)

## 5 užduotis (papildoma)
Perdaryti bet kurią ankstesnėse pamokose sukurtą arba savo programą, kurioje vartotojas turėjo įvesti duomenis, į programą su grafine sąsaja. Pvz., tą, kuri atrenka keliamuosius metus, skaičiuoja laiką nuo praeitos datos, pateikia informaciją apie įvestą eilutę ar pan.

![](https://github.com/StasysC/Python-2lvl/blob/master/Python/uzduotis5.jpg)
