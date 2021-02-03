## Užduotis: Tinklaraštis

### 1 etapas
Naudojantis Django framework'u sukurti tinklaraštį, kuris:
* Admin puslapyje leistų įvesti straipsnius (jie turi turėti pavadinimą, autorių, laiką ir tekstą).
* Teksto įvedimui panaudoti TinyMCE paketą, kad įraše būtų leidžiamas įrašyti ir atvaizduoti ne tik tekstas, bet ir  informacija html formatu.
* Sukurti puslapį, kuriame būtų atvaizduojami tinklaraščio įrašai. Naujausi būtų atvaizduojami viršuje. 
* Įrašai turi būti puslapiuojami.
* Leistų prie įrašo parašyti komentarą (kol kas - tik per Admin puslapį). Komentaras turi turėti vartotojo vardą, el. paštą (nebūtina), laiką ir tekstą.
* Pridėti papildomas Django pamokose išmoktas funkcijas (login puslapį, slaptažodžio keitimą ir t.t.).

### 2 etapas
* Padaryti, kad prisijungusiam vartotojui būtų leista kurti straipsnius (per CreateView).
* Padaryti, kad prisijungusiam vartotojui būtų leista redaguoti ir trinti savo straipsnius (per UpdateView ir DeleteView).
* Padaryti, kad prie kiekvieno straipsnio būtų matomas komentarų kiekis (parašyti atitinkamą @property metodą).
* Padaryti, kad straipsnių sąraše būtų matomos tik straipsnių santraukos (pvz. 2 eilučių) ir nuoroda "Skaityti daugiau". Ją paspaudus, būtų nukreipiama į pilną straipsnio aprašymą (DetailView).
* Prie komentaro modelio pridėti vartotojo lauką (ryšį su user). Padaryti, kad vartotojui leistų trinti ir redaguoti savo komentarus.
* Padaryti vertimus (puslapis turėtų būti dvejomis kalbomis, pvz. anglų, lietuvių). Padaryti kalbos perjungimo mygtuką.
***

[Atsakymas](https://github.com/DonatasNoreika/django_tinklarastis)