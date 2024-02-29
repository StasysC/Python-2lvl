# Pandas
Pandas yra duomenų analizės biblioteka, sukurta NumPy pagrindu. Pandas yra pagrindinis įrankis Python aplinkoje, skirtas duomenų analizei, išvalymui ir paruošimui. Pandas pasižymi sparta ir produktyvumu. Galima dirbti su duomenimis iš įvairių šaltinių.

Pandas diegiasi pip install pandas
```python
import numpy as np
import pandas as pd
```
## Serijos
Serijos (Series) yra smulkus pandas duomenų darinys, sukurtas ant NumPy array pagrindo.
```python
labels = ['x', 'y', 'z']
data = [20, 30, 40]
pd.Series(data=data)

0    20
1    30
2    40
dtype: int64
```
Matyti, kad nuo įprastų masyvų, pandas serija skiriasi tuo, kad turi indeksaciją. Vienas iš parametrų, kuriuos galime perduoti kurdami seriją yra index.
```python
pd.Series(data=data, index=labels)

x    20
y    30
z    40
dtype: int64
```
Pandas series galima kurti ir su python žodynais:
```python
zodynas = {'x':20, 'y':30, 'z':40}
pd.Series(zodynas)

x    20
y    30
z    40
dtype: int64
```
### Reikšmės traukimas iš serijos
```python
serija = pd.Series([1,2,3,4,5], ['Vilnius', 'Kaunas', 'Klaipėda', 'Panevėžys', 'Šiauliai'])
# atkreipkite dėmesį, kad duomenis galima sudėti nebūtinai nurodant parametro pavadinimą.

Vilnius      1
Kaunas       2
Klaipėda     3
Panevėžys    4
Šiauliai     5
dtype: int64
```
```python
serija['Vilnius']
# 1
```
### Operacijos su serijomis
```python
serija2 = pd.Series([1,2,3,4,5], ['Vilnius', 'Kaunas', 'Lentvaris', 'Šiauliai', 'Klaipėda'])
print(serija2)

Vilnius      1
Kaunas       2
Lentvaris    3
Šiauliai     4
Klaipėda     5
dtype: int64
```
naudojant sudėtį, pandas pagal galimybes bandys sumuoti reikšmes:
```python
serija + serija2

Kaunas       4.0
Klaipėda     8.0
Lentvaris    NaN
Panevėžys    NaN
Vilnius      2.0
Šiauliai     9.0
dtype: float64
```
Ten, kur pandos negalėjo atlikti sudėties veiksmo, sugeneravo NaN - not a number. Tiek Pandas, tiek NumPy mėgsta integer reikšmes versti į float, kad išlaikytų kiek įmanoma tikslesnę informaciją.

## DataFrames
DataFrames yra pagrindinis pandas operacijų objektas. Jeigu norime susikurti naują DF, reikia į parametrus perduoti data, index, columns:
```python
df = pd.DataFrame(np.random.rand(5,6), 
                  ['a', 'b', 'c', 'd', 'e'], 
                  ['U', 'V', 'W', 'X', 'Y', 'Z'])
     
        U        	V        	W       	X	        Y    	    Z
a	0.773002	0.559221	0.214122	0.979269	0.652045	0.804117
b	0.278172	0.248508	0.791801	0.030610	0.699674	0.773401
c	0.740262	0.057751	0.018922	0.682314	0.384986	0.099494
d	0.201956	0.846751	0.637614	0.537669	0.401869	0.601869
e	0.436100	0.326240	0.186233	0.101970	0.060907	0.151314
```
Kiekvienas stulpelis yra pandas serija, jos tarpusavyje dalijasi indeksais (a, b, c, d, e), pvz.:
```python
df['U']

a    0.361370
b    0.174726
c    0.605317
d    0.931402
e    0.113378
Name: U, dtype: float64
```
```python
type(df['U'])

# pandas.core.series.Series
```
### Jei norime daugiau stulpelių:
```python
df[['U', 'Y', 'Z']]

        U	        Y	        Z
a	0.361370	0.462288	0.504773
b	0.174726	0.128283	0.042082
c	0.605317	0.351447	0.072083
d	0.931402	0.232773	0.296398
e	0.113378	0.124420	0.666479
```
### Naujo stulpelio sukūrimas
```python
df['naujas'] = [1, 2, 3, 4, 5]

        U        	V        	W        	X        	Y        	Z	naujas
a	0.361370	0.902063	0.702827	0.986880	0.462288	0.504773	1
b	0.174726	0.518000	0.119260	0.839525	0.128283	0.042082	2
c	0.605317	0.887836	0.094214	0.327027	0.351447	0.072083	3
d	0.931402	0.905410	0.531652	0.587163	0.232773	0.296398	4
e	0.113378	0.060269	0.325921	0.646713	0.124420	0.666479	5
```
### Stulpelio ištrynimas
```python
df.drop('naujas', axis=1)

        U        	V        	W        	X        	Y        	Z
a	0.361370	0.902063	0.702827	0.986880	0.462288	0.504773
b	0.174726	0.518000	0.119260	0.839525	0.128283	0.042082
c	0.605317	0.887836	0.094214	0.327027	0.351447	0.072083
d	0.931402	0.905410	0.531652	0.587163	0.232773	0.296398
e	0.113378	0.060269	0.325921	0.646713	0.124420	0.666479
```
axis=0 reikštų, kad atliekame veiksmą su eilute. 1 tuo tarpu reiškia stulpelį.

### Inplace parametras

paskutinis mūsų veiksmas originalaus šaltinio nepakeitė, jeigu dabar išsikviesime df, matysime, kad jis koks buvo, toks ir liko:
```python

        U        	V         W        	X        	Y         Z	naujas
a	0.361370	0.902063	0.702827	0.986880	0.462288	0.504773	1
b	0.174726	0.518000	0.119260	0.839525	0.128283	0.042082	2
c	0.605317	0.887836	0.094214	0.327027	0.351447	0.072083	3
d	0.931402	0.905410	0.531652	0.587163	0.232773	0.296398	4
e	0.113378	0.060269	0.325921	0.646713	0.124420	0.666479	5
```
norėdami pakeisti originalą, turime nurodyti parametrą inplace=True:
```python
df.drop('naujas', 1, inplace=True)

        U        	V        	W         X        	Y        	Z
a	0.361370	0.902063	0.702827	0.986880	0.462288	0.504773
b	0.174726	0.518000	0.119260	0.839525	0.128283	0.042082
c	0.605317	0.887836	0.094214	0.327027	0.351447	0.072083
d	0.931402	0.905410	0.531652	0.587163	0.232773	0.296398
e	0.113378	0.060269	0.325921	0.646713	0.124420	0.666479
```
inplace parametras apsaugo mus nuo netyčinio duomenų sugadinimo

### Pabandykime ištrinti eilutę:
```python
df.drop('e')

        U        	V	        W	        X	        Y	        Z
a	0.361370	0.902063	0.702827	0.986880	0.462288	0.504773
b	0.174726	0.518000	0.119260	0.839525	0.128283	0.042082
c	0.605317	0.887836	0.094214	0.327027	0.351447	0.072083
d	0.931402	0.905410	0.531652	0.587163	0.232773	0.296398
```
trinant eilutę parametro axis=0 nurodyti nebūtina, tai yra default reikšmė

### Eilučių traukimas
```python
df.loc['e']

U    0.113378
V    0.060269
W    0.325921
X    0.646713
Y    0.124420
Z    0.666479
Name: e, dtype: float64
```
eilutes galime traukti ir pagal indeksą:
```python
df.iloc[4]

U    0.113378
V    0.060269
W    0.325921
X    0.646713
Y    0.124420
Z    0.666479
Name: e, dtype: float64
```
### Subsets

jeigu norime pavienės reikšmės iš lentelės:
```python
df.loc['c', 'Z']

0.07208345176824538
```
jeigu norime fragmento iš eilučių ir stulpelių (subset):
```python
df.loc[['a', 'c'], ['U', 'V', 'Z']]

        U	        V	        Z
a	0.361370	0.902063	0.504773
c	0.605317	0.887836	0.072083
```
### Duomenų traukimas pagal sąlygą:

duomenų traukimas pagal sąlygą yra labai panašus, kaip ir NumPy:
```python

        U	        V	        W	        X	        Y	        Z
a	0.361370	0.902063	0.702827	0.986880	0.462288	0.504773
b	0.174726	0.518000	0.119260	0.839525	0.128283	0.042082
c	0.605317	0.887836	0.094214	0.327027	0.351447	0.072083
d	0.931402	0.905410	0.531652	0.587163	0.232773	0.296398
e	0.113378	0.060269	0.325921	0.646713	0.124420	0.666479
```
```python
df[df>0.4]
 
      U	            V	      W	       X	        Y	        Z
a	  NaN	    0.902063	0.702827	0.986880	0.462288	0.504773
b	  NaN	    0.518000	   NaN	  0.839525	   NaN	    NaN
c	0.605317	0.887836	   NaN	    NaN	       NaN	    NaN
d	0.931402	0.905410	0.531652	0.587163	   NaN	    NaN
e	  NaN	      NaN	      NaN	    0.646713	   NaN	  0.666479
```
kur reikšmės atitinką sąlygą, turime reikšmes, kur neatitinka - NaN.

jeigu prireiktų subset'o, kur stulpelio 'W' reikšmės yra > 0.5:
```python
df[df['W']>0.5]

        U	        V	        W	        X	        Y	        Z
a	0.361370	0.902063	0.702827	0.986880	0.462288	0.504773
d	0.931402	0.905410	0.531652	0.587163	0.232773	0.296398
```
Skirtumas tarp šių operacijų toks, kad kai sąlygą taikome visam DataFrame'ui, gauname tą patį DataFrame su NaN reikšmėmis, tose vietose, kur originalios reikšmės neatitinka sąlygos. Kai sąlygą taikome stulpeliams, gauname tik tas eilutes, kurios atitinka sąlygą, t.y. vykdome filtravimą.

### Užklausų kombinavimas
```python
df[df['W']>0.5][['U', 'W', 'Z']]

        U	        W	        Z
a	0.361370	0.702827	0.504773
d	0.931402	0.531652	0.296398
```
šiame pavyzdyje gauname rezultatą, kokį gautumėm paeiliui ivykdę dvi atskiras eilutes: df1 = df[df['W']>0.5], df1[['U', 'W', 'Z']]. Užklausų kombinavimas leidžia mums nekurti atmintyje papildomų kintamųjų (kaip šiuo atveju df1).

### Sąlygų kombinavimas
```python
        U	        V	        W	        X	        Y	        Z
a	0.361370	0.902063	0.702827	0.986880	0.462288	0.504773
b	0.174726	0.518000	0.119260	0.839525	0.128283	0.042082
c	0.605317	0.887836	0.094214	0.327027	0.351447	0.072083
d	0.931402	0.905410	0.531652	0.587163	0.232773	0.296398
e	0.113378	0.060269	0.325921	0.646713	0.124420	0.666479
```
```python
df[(df['U']>0.5) & (df['Z']<0.5)]

        U	        V	        W	        X	        Y	        Z
c	0.605317	0.887836	0.094214	0.327027	0.351447	0.072083
d	0.931402	0.905410	0.531652	0.587163	0.232773	0.296398
```
gavome tas eilutes, kuriose U stulpelyje reikšmės didesnės, o Z stulpelyje mažesnės už 0.5.
```python
df[(df['U']>0.5) & (df['Z']<0.5)][['U', 'Z']]

        U	        Z
c	0.605317	0.072083
d	0.931402	0.296398
```
Čia sukombinavome dvi sąlygas ir iš rezultato paprašėme tik 2jų stulpelių

### Operacijos su index stulpeliu

reset_index paverčia mūsų seną indeksą dar vienu stulpeliu, ir sukuria naują indeksą iš skaičių. Reikia naudoti inplace=True, jei norime pakeisti originalą.
```python
df.reset_index()

  index	      U	        V	        W	        X	        Y	        Z
0	  a	  0.361370	0.902063	0.702827	0.986880	0.462288	0.504773
1	  b	  0.174726	0.518000	0.119260	0.839525	0.128283	0.042082
2	  c	  0.605317	0.887836	0.094214	0.327027	0.351447	0.072083
3	  d	  0.931402	0.905410	0.531652	0.587163	0.232773	0.296398
4	  e	  0.113378	0.060269	0.325921	0.646713	0.124420	0.666479
```
Norint sukurti naują indeksą, reikia pridėti naują stulpelį:
```python
naujas_indeksas = 'Vilnius Kaunas Klaipėda Šiauliai Panevėžys'.split()

['Vilnius', 'Kaunas', 'Klaipėda', 'Šiauliai', 'Panevėžys']

df['Miestai'] = naujas_indeksas

        U	        V	        W	        X	        Y	        Z	  Miestai
a	0.361370	0.902063	0.702827	0.986880	0.462288	0.504773	Vilnius
b	0.174726	0.518000	0.119260	0.839525	0.128283	0.042082	Kaunas
c	0.605317	0.887836	0.094214	0.327027	0.351447	0.072083	Klaipėda
d	0.931402	0.905410	0.531652	0.587163	0.232773	0.296398	Šiauliai
e	0.113378	0.060269	0.325921	0.646713	0.124420	0.666479	Panevėžys

df.set_index('Miestai')

              U	      V	          W	        X	        Y	        Z
Miestai						
Vilnius 	0.361370	0.902063	0.702827	0.986880	0.462288	0.504773
Kaunas	  0.174726	0.518000	0.119260	0.839525	0.128283	0.042082
Klaipėda	0.605317	0.887836	0.094214	0.327027	0.351447	0.072083
Šiauliai	0.931402	0.905410	0.531652	0.587163	0.232773	0.296398
Panevėžys	0.113378	0.060269	0.325921	0.646713	0.124420	0.666479
```
# Užduotys
## 1 užduotis
Nuskaitykite į **df** failą 'miestai isvalyti.csv', failą rasite [čia](https://github.com/StasysC/Python-2lvl/blob/master/Python/miestai_isvalyti.csv) ir atlikite šiuos veiksmus:
* Atspausdinkite pirmas penkias **df** eilutes
* Padarykite, kad indeksas būtų stulpelis 'Miestas', ir kad šis pasikeitimas išliktų originale
* Ištraukite reikšmę, kiek gyventojų gyveno Marijampolėje 1923 m.
* Ištraukite stulpelį '1897' ir atspausdinkite pirmas penkias eilutes
* Ištraukite stulpelius '2019', '1970', '1923' ir atspausdinkite pirmas 10 eilučių
* Pridėkite stulpelį su numeracija
* Ištraukite miestus nuo 30 iki 39 pozicijos
* Ištraukite miestus kurių dar nebuvo 1959 m.
* Ištraukite miestus kurie 1897 m. turėjo daugiau gyventojų, negu 2019 m.
* Ištraukite miestus kuriuose nuo 2011 m. iki 2019 m. padaugėjo gyventojų 
* Ištraukite miestus kuriuose gyventojų skaičius nuosekliai mažėjo nuo pat 1897 m.
* Suraskite labiausiai procentaliai gyventojų skaičiumi padidėjusį ir sumažėjusį miestus nuo 1989 m. (pagalba - naudokite .idxmax() .idxmin, .max() ir .min() funkcijas.)
* Nuresetinkite indeksą
