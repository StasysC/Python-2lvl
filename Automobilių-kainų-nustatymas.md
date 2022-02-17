## užduotis
## 1 etapas
* Sukurti programą, kuri paimtų pagrindinę informaciją iš Autoplius.lt (galite Domoplius ar kitos, jei mašinytės nedomina) skelbimų: markę, modelį, variklio turį, metus, galią, ridą, kėbulą (žr. Web Scraping paskaitą).
* Įrašyti visą informaciją į csv failą ar duomenų bazę.
* Sutvarkyti duomenis, kad jie stulpeliuose būtų tinkamu formatu, skaičiai o ne stringais (žr. Pandas paskaitą).
* Vizualizuoti norimus duomenis (su Seaborn).

**Dėmesio: jei per web scraping pradėsite skenuoti visus Autoplius puslapius iš eilės, serveriui gali pasidaryti įtartina ir jis gali jūsų IP užblokuoti :) Todėl pradžiai nuskenuokite pvz. tik vieną puslapį į csv ir dirbkite su juo. Vėliau, kai skenuosite visus puslapius, padarykite random pauzę tarp kiekvieno puslapio skenavimo (taip procesas, užtruks gerokai ilgiau, bet saugiau). Be to, nebūtina skenuoti visų 30000+ skelbimų. Galima pavyzdžiui skenuoti tik šios dienos skelbimus (apie 1000).**

## 2 etapas
* Paruošti duomenis darbui su machine learning (performuoti string stulpelius į dummies), išimti, jei ko nereikia. Modelis turės pagal automobilio informaciją atspėti kainą. 
* Paduoti paruoštus duomenis machine learning modeliui, patikrinti apmokyti modelio efektyvumą. Jei jis prastas, pakoreguoti paduodamus duomenis ir vėl iš naujo apmokyti modelį, kol rezultatas bus norimas.
* Išsaugoti apmokytą modelį faile (pickle).
* Išbandyti modelį realiais pavyzdžiais, paduodant jam realius duomenis.
* Sukurti vartotoją sąsają (GUI, su konsole, tkinter ar Flask), per kurią vartotojas galėtų įvesti savo automobilio duomenis ir sužinoti apmokyto modelio spėjamą kainą.