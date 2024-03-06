# Flask kaip vartotojo sąsaja

Čia bus trumpas supažindinimas su Flask mikro karkasu, kaip jam padedant naudoti naršyklę, kaip vartotojo sąsają. Pažintis apims tik pačius pagrindus - kaip atvaizduoti informaciją šablone(template), kaip iš jo priimti vartotojo duomenis. Karkasas diegiasi *pip install Flask*.

## Pradžia

app.py:
```python
from flask import Flask, render_template
# iš flask bibliotekos importuojame klasę Flask ir f-ją render_template.
app = Flask(__name__)
# inicijuojame klasės Flask objektą, priskiriame kintamąjam app.

@app.route('/')
# įvelkame f-ją į flask dekoratorių. Be jo  funkcija būtų bereikšmė. Dekorato riaus parametruose nurodome, kad norėsime rezultato 127.0.0.1:8000/ url adrese."""

def index():
    return render_template('index.html')
# funkcijoje index nurodome, kad norėsime sugeneruoti index.html

if __name__ == '__main__':
  app.run(host='127.0.0.1', port=8000, debug=True)

# patikrinę, ar programa leidžiama ne iš kito failo, leidžiame mūsų app, su parametrais. debug = True klaidos atveju mums rodys informatyvias žinutes naršyklėje. 
```

Komentaruose šiek tiek informacijos, kas vyksta. Dabar mums reikės susikurti html šabloną. Flask šablonų ieško templates kataloge. :

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Demo</title>
</head>
<body>
    <h1>Flask Flask Flask</h1>
</body>
</html>
```

Patikrinkime, ar veikia:

![](https://github.com/robotautas/kursas/blob/master/Flask/MDs/1%20dalis/flaskflaskflask.png)

### Logikos naudojimas šablonuose:

Už logiką šablonuose atsako Jinja2 šablonų generatorius (templating engine), jis per savo sintaksę leidžia mums įterpti kintamuosius ir logiką į html failus. 

paruoškime paprastą žodynų sąrašą, kuris galės būti mūsų duomenų bazės imitacija:

dictionary.py:

```python
data =[{
    'data':'2020 01 01',
    'autorius': 'Autorius 1',
    'pavadinimas': 'Apie nieką',
    'tekstas': 'Zombie ipsum reversus ab viral inferno, nam rick grimes malum cerebro. De carne lumbering animata corpora quaeritis. Summus brains sit​​, morbo vel maleficia? De apocalypsi gorger omero undead survivor dictum mauris.'
},
{
    'data':'2020 02 01',
    'autorius': 'KITAS AUTORIUS',
    'pavadinimas': 'Apie zombius',
    'tekstas': 'Zombie ipsum reversus ab viral inferno, nam rick grimes malum cerebro. De carne lumbering animata corpora quaeritis. Summus brains sit​​, morbo vel maleficia? De apocalypsi gorger omero undead survivor dictum mauris. '
},
{
    'data':'2020 03 01',
    'autorius': 'Dar kažkas',
    'pavadinimas': 'Braiiins!',
    'tekstas': 'Zombie ipsum reversus ab viral inferno, nam rick grimes malum cerebro. De carne lumbering animata corpora quaeritis. Summus brains sit​​, morbo vel maleficia? De apocalypsi gorger omero undead survivor dictum mauris.' 
}]
```

Pagrindiniame faile importuokime šį kintamąjį ir perduokime į šabloną:

app.py:

```python
from flask import Flask, render_template
from dictionary import data # IMPORTUOJAME
app = Flask(__name__)


@app.route('/')

def index():
    return render_template('index.html', data=data) # PERDUODAME Į ŠABLONĄ

if __name__ == '__main__':
  app.run(host='127.0.0.1', port=8000, debug=True)
```

Dabar dirbsime su šablonu. Pradžiai tiesiog perduokime kintamąjį į *body*:

```html
<body>
    <h1>Straipsniai:</h1>
    {{ data }}  
</body>
```

![](https://github.com/robotautas/kursas/blob/master/Flask/MDs/1%20dalis/perduotas1_kintamasis.png)

Čia yra grubus žodynų sąrašo perdavimas, jį ir matome. Pabandykime tai paversti straipsnių puslapiu:

```html
<body>
    <h1>Straipsniai</h1>
    <br><br>
    {% for straipsnis in data %}
    <h3>{{ straipsnis['pavadinimas'] }}</h3>
    <p>{{ straipsnis['data'] }}, {{ straipsnis['autorius'] }}</p>
    <hr>
    <p>{{ straipsnis['tekstas'] }}</p>
    <hr>    
    {% endfor %}
</body>
```

![](https://github.com/robotautas/kursas/blob/master/Flask/MDs/1%20dalis/straipsniai.png)

Matome, kaip galime iteruoti per duomenis html'e. Pamėginkime įtraukti if logiką. Pradžiai papildykime 'duomenų bazę'. Kiekviename žodyne įtraukime 'status'. Dalies statusas bus 'published', dalies 'unpublished':

```python
{
    'data':'2020 01 01',
    'autorius': 'Autorius 1',
    'pavadinimas': 'Apie nieką',
    'tekstas': 'Zombie ipsum reversus ab viral inferno, nam rick grimes malum cerebro. De carne lumbering animata corpora quaeritis. Summus brains sit​​, morbo vel maleficia? De apocalypsi gorger omero undead survivor dictum mauris.',
    'status': 'published'
}, # ir t.t.
```

įtraukime if logiką į šabloną:

```html
<body>
    <h1>Straipsniai</h1>
    <br>
    {% for straipsnis in data %}
    {% if straipsnis['status'] == 'published' %}
    <h3>{{ straipsnis['pavadinimas'] }}</h3>
    <p>{{ straipsnis['data'] }}, <i>{{ straipsnis['autorius'] }}</i></p>
    <hr>
    <p>{{ straipsnis['tekstas'] }}</p>
    <br><br> 
    {% endif %}
    {% endfor %}
</body>
```

![](https://github.com/robotautas/kursas/blob/master/Flask/MDs/1%20dalis/su_if.png)

Matome, kad straipsnis su statusu != 'published' nebuvo publikuotas.
Kaip ir python'e, galima naudoti *{%elif %}* ir *{% else %}*. Pvz.:

```html
<body>
    <h1>Straipsniai</h1>
    <br>
    {% for straipsnis in data %}
    {% if straipsnis['status'] == 'published' %}
    <h3>{{ straipsnis['pavadinimas'] }}</h3>
    <p>{{ straipsnis['data'] }}, <i>{{ straipsnis['autorius'] }}</i></p>
    <hr>
    <p>{{ straipsnis['tekstas'] }}</p>
    <br><br>
    {% else %}
    <h3>{{ straipsnis['pavadinimas'] }} - <i>Publikavimas laikinai išjungtas</i></h3>
    <br><br>
    {% endif %}
    {% endfor %}
</body>
```

## Vartotojo duomenų nuskaitymas 

papildykime šabloną įvesties langeliu ir mygtuku:

```html
<body>
    <form method="POST">
        <label for="Input">Įveskite straipsnių skaičių: </label>
        <input id="Input" name="number">
        <input type="submit" value="Submit">
    </form>
    .....
```

modifikuokime savo app.py:

```python
@app.route('/', methods=['GET', 'POST']) # standartinė praktika, kuomet tikimės užklausų
def index():
    if request.method == 'POST': # tikriname, ar yra užklausa
        number = request.form['number']
        data_modified = data[:int(number)]
    return render_template('index.html', data=data_modified
```

Čia yra paprastas pavyzdys, kaip galime dirbti su vartotojo įvestais duomenimis. Aplikacijos logika paprasta, tačiau nėra ribų, kiek galime ją plėsti.

# Užduotys (pasipraktikavimui :)
## 1 užduotis
Sukurti programą, kuri turėtų statinį puslapį, pvz. localhost:5000 su norimu tekstu (rekomenduojama naudoti šablonus)

## 2 užduotis
Sukurti programą, kuri įvedus norimą žodį langelyje ir nuspaudus mygtuką, atspausdintų jį penkis kartus.

## 3 užduotis
Sukurti programą, kuri leistų įvesti metus ir paspaudus patvirtinimo mygtuką parodytų, ar jie yra keliamieji.

## 4 užduotis
sukurkite kūno masės indekso skaičiuoklę
