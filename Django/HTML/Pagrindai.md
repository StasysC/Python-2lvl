# HTML puslapio struktūra
HTML (*HyperText Markup Language*) yra pats pagrindinis žiniatinklio kūrimo elementas. Jis apibrėžia interneto turinio prasmę ir struktūrą. Kitos technologijos, išskyrus HTML, paprastai naudojamos aprašyti tinklalapio išvaizdą / pristatymą (CSS) arba funkcionalumą / elgesį (JavaScript).

**HTML nėra programavimo kalba, tai žymėjimo kalba!**

# HTML elemento anatomija
Prieš pradedant rašyti kodą, jums reikia susikurti HTML failą:
* Atsidarykite code editor kurį norite naudoti (WebStorm, Sublime, VS Code, Notepad++, etc…);
* Spauskite Ctrl/CMD + S;
* Išsaugokite failą pavadinimu index.html (.html yra failo plėtinys nurodantis jog tai bus būtent HTML  failas o ne joks kitoks);
* Pradėkite rašyti kodą.

Turime tekstą „My cat is very grumpy“. 

HTML kalbos atveju jis atrodytų taip:
```html
<p>My cat is very grumpy</p>
```
![image](https://github.com/StasysC/Python-2lvl/blob/master/Django/HTML/Grumpy_cat.png)

Elementai taip pat gali turėti atributus. Atributuose yra papildomos informacijos apie elementą, kurios nenorite rodyti tikrame turinyje. Atributai atrodo taip:

![image](https://github.com/StasysC/Python-2lvl/blob/master/Django/HTML/class.png)

Čia „class“ yra atributo pavadinimas, o „editor-note“ atributo vertė. Beje, „class“ atributas leidžia suteikti elementui identifikatorių, kurį galima naudoti norint jį (ir visus kitus tos pačios klasės vertės elementus) nukreipti su stiliaus informacija ir kitais dalykais.

Jūs taip pat galite įdėti elementus į kitus elementus - tai vadinama (angl.) “nesting”. Jei norėtume konstatuoti, kad mūsų katė yra labai niūri, žodį „very“ galėtume įvynioti į **```<strong>```** elementą, o tai reiškia, kad šis žodis turi būti stipriai pabrėžtas:
```html
<p>My cat is <strong>very</strong> grumpy.</p>
```
Svarbu atkreipti dėmesį ar mūsų elementai yra tinkamai talpinami vienas kitame.

Negalima: ```<p>My cat is <strong>very grumpy.</p></strong>```
Galima: ```<p>My cat is <strong>very</strong> grumpy.</p>```

![image](https://github.com/StasysC/Python-2lvl/blob/master/Django/HTML/htm_struct.png)

<! DOCTYPE html> – tai yra būtina preambulė
<html> </html> – šis apgaubia visą turinį visame puslapyje ir kartais vadinamas elementas “root” elementu.
<head> </head> – šis elementas veikia kaip visų dalykų, kuriuos norite įtraukti į HTML puslapį, talpykla, kurie nėra turinys, kurį rodote savo puslapio lankytojams. Tai apima tokius dalykus kaip raktiniai žodžiai ir puslapio aprašymas, kurį norite rodyti paieškos rezultatuose, CSS, kad stilizuotų mūsų turinį, simbolių rinkinio deklaracijos ir kt.
<meta charset = "utf-8"> – šis elementas nustato simbolių rinkinį, kurį jūsų dokumentas turėtų naudoti į UTF-8, kuriame yra dauguma simbolių iš daugumos rašytinių kalbų. Iš esmės dabar jis gali tvarkyti bet kokį tekstinį turinį, kurį galite įdėti. Nėra jokios priežasties to nenustatyti ir tai gali padėti išvengti kai kurių problemų vėliau.
<title> </title> – tai nustato jūsų puslapio pavadinimą, kuris rodomas naršyklės skirtuke.
<body> </body> – čia yra visas turinys, kurį norite parodyti interneto vartotojams, kai jie lankosi jūsų puslapyje, nesvarbu, ar tai tekstas, nuotraukos, vaizdo įrašai, žaidimai, grojami garso takeliai ar dar kas kita.

# HTML žymos (angl. tags)
### Teksto žymėjimas – Antraštės
Antraštės elementai leidžia nurodyti, kad tam tikros turinio dalys yra antraštės. HTML yra 6 antraštės lygiai, ```<h1> - <h6>```
Pvz:
* ```html
  <h1>My main title</h1>
  ```
* ```html
  <h2>My top level heading</h2>
  ```
* ```html
  <h3>My subheading</h3>
  ```
* ```html
  <h4>My sub-subheading</h4> 
  ```


### Teksto žymėjimas – Tekstas
Elementai ```<p>``` skirti teksto pastraipoms laikyti

Pvz.:  
```
<p>Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy
text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book. It has
survived not only five centuries, but also the leap into electronic typesetting, remaining essentially unchanged. It was popularised in the
1960s with the release of Letraset sheets containing Lorem Ipsum passages, and more recently with desktop publishing software like
Aldus PageMaker including versions of Lorem Ipsum.</p>
```
  
### Teksto žymėjimas – Nuorodos
Nuorodos yra labai svarbios – jos daro internetą – tinklu! Norėdami pridėti nuorodą, turime naudoti paprastą elementą – ```<a>```, kuris yra trumpa "anchor" forma. Norėdami, kad pastraipos tekstas taptų nuoroda, reikia atlikti šiuos veiksmus:
1. Pasirinkti tekstą. Pavyzdžiui "Google".
2. Apvynioti tekstą <a> elemente, kaip parodyta žemiau:
```html <a> Google </a> ```
3. Suteikti elementui <a> 'href' atributą, kaip parodyta žemiau:
```html <a href="">Google</a> ```
4. Užpildyti šio atributo vertę žiniatinklio adresu, į kurį norima susieti nuorodą:
```html <a href="https://google.com">Google</a> ``` (jeigu href aprašysite puslapio link‘ą be ```https://``` tuomet puslapis neužsikraus, tad
visuomet atsiminkite, kad ```www.``` nėra būtinas, tačiau ```https://``` – privalomas.
  
### Žymėjimas – Paveikslėliai
Paveikslėliai kuriami naudojant <img> arba <picture> elementus. Į mūsų puslapį jie įterpia vaizdą toje vietoje, kurioje jie nurodomi.
  Naudojant:
  <img> - tai daroma per atributą src(source), kuriame yra kelias į mūsų nuotrauką, pvz:
  ```html
  <img src=images/firefox-icon.png" alt="My test image> 
  ```
  <picture> - tai darome per <source> ir <img> elementus. Naršyklė įvertins kiekvieną <source> elementą ir parinks geriausiai atitinkantį situaciją tarp jų. Jei atitiktys nerandamos arba naršyklė nepalaiko elemento <picture>, pasirenkamas <img> elemento src atributo URL, pvz: 
    ```html
    <picture>
      <source srcset="URL/file directory" media="(min-width: 800px)">
      <img src="URL/file directory" alt="" />
    </picture>
    ```
 Papildomai:
Picture vs img: https://blog.bitsrc.io/why-you-should-use-picture-tag-instead-of-img-tag-b9841e86bf8b

    Teksto žymėjimas – Sąrašai
Daugybė žiniatinklio turinio yra sąrašai, o HTML turi specialių elementų. Sąrašų žymėjimas visada susideda iš mažiausiai 2 elementų. Dažniausi sąrašų tipai yra suskirstyti ir ne suskirstyti sąrašai:
Nesuskirstyti (angl. unordered) yra sąrašai, kuriuose elementų eilės tvarka yra nesvarbi, pvz., Pirkinių sąrašas. Jie suvynioti į
<ul> elementą.
  Suskirstyti (angl. ordered) yra sąrašai, kur svarbi elementų tvarka, pavyzdžiui, receptas. Jie suvynioti į elementą <ol>.
  Kiekvienas elementas sąrašuose dedamas į <li> elementą	(sąrašo elementas).


