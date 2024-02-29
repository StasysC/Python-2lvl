# Pandas II dalis
```python
import numpy as np
import pandas as pd
```
## Trūkstami duomenys
Susikursime pavyzdį:
```python
df = pd.DataFrame(np.random.rand(5,6), 
                  ['a', 'b', 'c', 'd', 'e'], 
                  ['U', 'V', 'W', 'X', 'Y', 'Z'])

        U	        V	        W	        X	        Y	        Z
a	0.551877	0.091217	0.141880	0.163693	0.589571	0.275082
b	0.219124	0.023263	0.049307	0.196051	0.134534	0.772043
c	0.406546	0.643218	0.966651	0.807019	0.002305	0.498210
d	0.653695	0.182275	0.742331	0.637394	0.804578	0.678703
e	0.082644	0.371362	0.476152	0.464577	0.677104	0.294346
```
```python
table = df[df>.15]

        U    	    V	        W	        X	        Y	        Z
a	0.551877	  NaN	      NaN	    0.163693	0.589571	0.275082
b	0.219124	  NaN	      NaN	    0.196051	  NaN	    0.772043
c	0.406546	0.643218	0.966651	0.807019	  NaN    	0.498210
d	0.653695	0.182275	0.742331	0.637394	0.804578	0.678703
e	  NaN    	0.371362	0.476152	0.464577	0.677104	0.294346
```
Funkcija, padėsianti mums aptikti nulines reikšmes yra .isnull(). Naudojimo pavyzdžiai:
```python
table.isnull() # grąžina lentelę, kur true reikšmės yra NaN

    U	    V	    W	    X	    Y	    Z
a	False	True	True	False	False	False
b	False	True	True	False	True	False
c	False	False	False	False	True	False
d	False	False	False	False	False	False
e	True	False	False	False	False	False
```
```python
table.isnull().sum() # Rodo kiek kuriame stulpelyje NaN reikšmių

U    1
V    2
W    2
X    0
Y    2
Z    0
dtype: int64
```
```python
table['V'].isnull() # Galima tikrinti atskiruose stulpeliuose

a     True
b     True
c    False
d    False
e    False
Name: V, dtype: bool
```
```python
table['V'].isnull().sum()
# 2
```
pirmas metodas tvarkytis su trūkstamais duomenimis yra **.dropna()** jis išmeta visas eilutes, kuriose yra bent viena NaN reikšmė:
```python
table.dropna()

        U	        V	        W	        X	        Y	        Z
d	0.653695	0.182275	0.742331	0.637394	0.804578	0.678703
```
jeigu norime išmesti stulpelius, turinčius bent vieną NaN, turime nurodyti ašį:
```python
table.dropna(axis=1)
        X	        Z
a	0.163693	0.275082
b	0.196051	0.772043
c	0.807019	0.498210
d	0.637394	0.678703
e	0.464577	0.294346
```
Galime išmesti tik tas eilutes, ar stulpelius, kurie turi mažiau, negu (pvz) 5 NE NaN reikšmes:
```python
table.dropna(thresh=5)

        U	        V	        W	        X	        Y	        Z
c	0.406546	0.643218	0.966651	0.807019	  NaN    	0.498210
d	0.653695	0.182275	0.742331	0.637394	0.804578	0.678703
e	  NaN	    0.371362	0.476152	0.464577	0.677104	0.294346
```
Papildomai nurodžius ašį, tą patį galima padaryti ir su stulpeliais.

Jei norime NaN reikšmes pakeisti kažkuo kitu, naudosime **.fillna()** metodą:
```python
table.fillna('bupkis')

        U	      V	      W	            X	        Y	        Z
a	0.551877	  bupkis	bupkis	  0.163693	0.589571	0.275082
b	0.219124	  bupkis	bupkis	  0.196051	  bupkis	0.772043
c	0.406546	0.643218	0.966651	0.807019	  bupkis	0.498210
d	0.653695	0.182275	0.742331	0.637394	0.804578	0.678703
e	  bupkis	0.371362	0.476152	0.464577	0.677104	0.294346
```
Daugiau prasmės būtų pakeisti pvz. stulpelio vidurkiu:
```python
table['W'].fillna(value=table['W'].mean())

a    0.728378
b    0.728378
c    0.966651
d    0.742331
e    0.476152
Name: W, dtype: float64
```
```python
table.fillna(value=table.mean())
        U	        V        	W	        X	        Y	        Z
a	0.551877	0.398952	0.728378	0.163693	0.589571	0.275082
b	0.219124	0.398952	0.728378	0.196051	0.690418	0.772043
c	0.406546	0.643218	0.966651	0.807019	0.690418	0.498210
d	0.653695	0.182275	0.742331	0.637394	0.804578	0.678703
e	0.457810	0.371362	0.476152	0.464577	0.677104	0.294346
```
## Grupavimas
Susikurkime pavyzdį:
```python
duomenys = {'Šalis': ['Lietuva',
  'Lietuva',
  'Lietuva',
  'Latvija',
  'Latvija',
  'Latvija',
  'Estija',
  'Estija',
  'Estija'],
 'Miestas': ['Vilnius',
  'Kaunas',
  'Klaipėda',
  'Ryga',
  'Ventspilis',
  'Daugpilis',
  'Talinas',
  'Tartu',
  'Pernu'],
 'Gyv': [541, 287, 147, 716, 43, 105, 400, 101, 46]}

data = pd.DataFrame(duomenys)

    Šalis	Miestas	    Gyv
0	Lietuva	Vilnius      541
1	Lietuva	Kaunas       287
2	Lietuva	Klaipėda     147
3	Latvija	Ryga         716
4	Latvija	Ventspilis   43
5	Latvija	Daugpilis    105
6	Estija	Talinas      400
7	Estija	Tartu        101
8	Estija	Pernu        46
```
panaudokime **.groupby()** metodą, viduje nurodydami stulpelį, pagal kurį grupuosime.
```python
data.groupby('Šalis')

<pandas.core.groupby.generic.DataFrameGroupBy object at 0x7fb9cf8000f0>
```
gavome groupby objektą, kuris turi savo metodus. Tam kad galėtumėm jais naudotis, priskirkime objektą kintamąjam:
```python
baltic = data.groupby('Šalis')

<pandas.core.groupby.generic.DataFrameGroupBy object at 0x7fb9cf7da278>
```python
**.mean()** skaičiuos mums vidurkį:
```python
baltic.mean()

            Gyv
Šalis	
Estija	182.333333
Latvija	288.000000
Lietuva	325.000000
```
**.sum()** sumuos:
```python
baltic.sum()
        Gyv
Šalis	
Estija	547
Latvija	864
Lietuva	975
```
iš groupby objekto galime trukti reikšmes tokiu būdu:

**.count()** suskaičiuos kiek yra įrašų grupės stulpeliuose:
```python
baltic.count()

        Miestas	Gyv
Šalis		
Estija	  3      3
Latvija	  3	     3
Lietuva	  3	     3
```
atkreipkite dėmesį, kad jeigu metodas negali atlikti veiksmo su stulpelio įrašais, rezultate to stulpelio ir nerodo. šiuo atveju galime suskaičiuoti string įrašus, todėl stulpelis 'Miestas' įtrauktas į rezultatą

**.max()** duos eilutę su maksimaliu, **.min()** su minimaliu rezultatais:
```python
baltic.max()

        Miestas	    Gyv
Šalis		
Estija	Tartu	      400
Latvija	Ventspilis	716
Lietuva	Vilnius	    541
```
```python
baltic.min()

        Miestas	    Gyv
Šalis		
Estija	Pernu	      46
Latvija	Daugpilis	  43
Lietuva	Kaunas	    147
```
šiuo atveju matome, kad miestų stulpelį išrūšiavo pagal abėcelę, o skaičius, kaip ir tikėjomės. Max ir min nėra labai praktiški su string tipo reikšmėmis.

iš groupby objektų galime traukti reikšmes:
```python
baltic.sum().loc['Lietuva']

Gyv    975
Name: Lietuva, dtype: int64
```
**.describe()** metodas duoda pagrindinę informaciją apie lentelės duomenis:
```python
baltic.describe()

                                                            Gyv
        count	mean	          std	  min	  25%	  50%	    75%	max
Šalis								
Estija	3.0	182.333333	190.500219	46.0	73.5	101.0	250.5	400.0
Latvija	3.0	288.000000	371.952954	43.0	74.0	105.0	410.5	716.0
Lietuva	3.0	325.000000	199.729818	147.0	217.0	287.0	414.0	541.0
```
galime sukeisti stulpelius su eilutėmis su **.transpose()**:
```python
baltic.describe().transpose()

Šalis	 Estija	      Latvija	    Lietuva
count	 3.000000	    3.000000	  3.000000
mean	182.333333	288.000000	325.000000
std	  190.500219	371.952954	199.729818
min	  46.000000	  43.000000	  147.000000
25%	  73.500000	  74.000000	  217.000000
50%	  101.000000	105.000000	287.000000
75%	  250.500000	410.500000	414.000000
max	  400.000000	716.000000	541.000000
```
jeigu domina vieno kurio nors stulpelio statistika, galime ją ištraukti taip:
```python
baltic.describe().transpose()['Estija']
Gyv  count      3.000000
     mean     182.333333
     std      190.500219
     min       46.000000
     25%       73.500000
     50%      101.000000
     75%      250.500000
     max      400.000000
Name: Estija, dtype: float64
```
## DF Jungimas
susikurkime pavyzdžius:
```python
data_main = data[0:6]

    Šalis	Miestas	    Gyv
0	Lietuva	Vilnius	    541
1	Lietuva	Kaunas	    287
2	Lietuva	Klaipėda	  147
3	Latvija	Ryga	      716
4	Latvija	Ventspilis	43
5	Latvija	Daugpilis	  105

data_bottom = data[6:]

  Šalis	  Miestas	Gyv
6	Estija	Talinas	400
7	Estija	Tartu	  101
8	Estija	Pernu	  46
```
norėdami sujungti data_main su data_bottom naudosime .concat() metodą, viduje įrašydami lentelių, kurias jungsime sąrašą:
```python
pd.concat([data_main, data_bottom])
    Šalis	Miestas	    Gyv
0	Lietuva	Vilnius	    541
1	Lietuva	Kaunas	    287
2	Lietuva	Klaipėda	  147
3	Latvija	Ryga	      716
4	Latvija	Ventspilis	43
5	Latvija	Daugpilis	  105
6	Estija	Talinas	    400
7	Estija	Tartu	      101
8	Estija	Pernu	      46
```
galime prijungti lentelę iš dešinės:
```python
pd.concat([data_main, data_bottom], axis=1)

  Šalis	Miestas	      Gyv	  Šalis	  Miestas	Gyv
0	Lietuva	Vilnius	    541.0	  NaN	    NaN	  NaN
1	Lietuva	Kaunas	    287.0	  NaN	    NaN	  NaN
2	Lietuva	Klaipėda	  147.0	  NaN	    NaN	  NaN
3	Latvija	Ryga	      716.0	  NaN	    NaN	  NaN
4	Latvija	Ventspilis	43.0	  NaN	    NaN	  NaN
5	Latvija	Daugpilis	  105.0	  NaN	    NaN	  NaN
6	  NaN	    NaN	        NaN	Estija	Talinas	400.0
7	  NaN	    NaN	        NaN	Estija	Tartu	  101.0
8	  NaN	    NaN	        NaN	Estija	Pernu	  46.0
```
matome, kad pandas ieškojo antroje lentelėje sutampančių indeksų, ir neradus atliko jungimą užpildant tuščias vietas NaN. Todėl jungiant, reikia įsitikinti, kad jungimui tinka abi pusės. Pertvarkykime data_right indeksą:

data_right = data_bottom.reset_index()
data_right.drop(columns='index', inplace=True)
data_right
Šalis	Miestas	Gyv
0	Estija	Talinas	400
1	Estija	Tartu	101
2	Estija	Pernu	46
pd.concat([data_main, data_right], axis=1)
Šalis	Miestas	Gyv	Šalis	Miestas	Gyv
0	Lietuva	Vilnius	541	Estija	Talinas	400.0
1	Lietuva	Kaunas	287	Estija	Tartu	101.0
2	Lietuva	Klaipėda	147	Estija	Pernu	46.0
3	Latvija	Ryga	716	NaN	NaN	NaN
4	Latvija	Ventspilis	43	NaN	NaN	NaN
5	Latvija	Daugpilis	105	NaN	NaN	NaN
dabar pandas surado sutampančius indeksus, tačiau visvien turime NaN reikšmes, kadangi lentelėje trūksta duomenų. Pridėkime papildomų eilučių:

lenkija = {'Šalis': ['Lenkija', 'Lenkija', 'Lenkija'], 
           'Miestas':['Varšuva', 'Vroclavas', 'Gdanskas'], 
          'Gyv': [1688, 638, 461]}
pl = pd.DataFrame(lenkija)
data_right1 = pd.concat([data_right, pl])
data_right = data_right1.reset_index().drop(columns='index')
data_right
Šalis	Miestas	Gyv
0	Estija	Talinas	400
1	Estija	Tartu	101
2	Estija	Pernu	46
3	Lenkija	Varšuva	1688
4	Lenkija	Vroclavas	638
5	Lenkija	Gdanskas	461
Pabandykime sujungti data_main su data_right :)

pd.concat([data_main, data_right], 1)
Šalis	Miestas	Gyv	Šalis	Miestas	Gyv
0	Lietuva	Vilnius	541	Estija	Talinas	400
1	Lietuva	Kaunas	287	Estija	Tartu	101
2	Lietuva	Klaipėda	147	Estija	Pernu	46
3	Latvija	Ryga	716	Lenkija	Varšuva	1688
4	Latvija	Ventspilis	43	Lenkija	Vroclavas	638
5	Latvija	Daugpilis	105	Lenkija	Gdanskas	461
.merge()

Jeigu data_main ir data_right turėtų po vieną sutampantį stulpelį, pvz.:

key = 'A B C D E F'.split()
data_main['key'] = key
data_right['key'] = key
/usr/lib/python3/dist-packages/ipykernel_launcher.py:2: SettingWithCopyWarning: 
A value is trying to be set on a copy of a slice from a DataFrame.
Try using .loc[row_indexer,col_indexer] = value instead

See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
  
data_main
Šalis	Miestas	Gyv	key
0	Lietuva	Vilnius	541	A
1	Lietuva	Kaunas	287	B
2	Lietuva	Klaipėda	147	C
3	Latvija	Ryga	716	D
4	Latvija	Ventspilis	43	E
5	Latvija	Daugpilis	105	F
data_right
Šalis	Miestas	Gyv	key
0	Estija	Talinas	400	A
1	Estija	Tartu	101	B
2	Estija	Pernu	46	C
3	Lenkija	Varšuva	1688	D
4	Lenkija	Vroclavas	638	E
5	Lenkija	Gdanskas	461	F
galima jas sulieti to bendro stulpelio pagrindu:

pd.merge(data_main, data_right, on='key')
Šalis_x	Miestas_x	Gyv_x	key	Šalis_y	Miestas_y	Gyv_y
0	Lietuva	Vilnius	541	A	Estija	Talinas	400
1	Lietuva	Kaunas	287	B	Estija	Tartu	101
2	Lietuva	Klaipėda	147	C	Estija	Pernu	46
3	Latvija	Ryga	716	D	Lenkija	Varšuva	1688
4	Latvija	Ventspilis	43	E	Lenkija	Vroclavas	638
5	Latvija	Daugpilis	105	F	Lenkija	Gdanskas	461
matome, kad lentelės suklijuotos, tačiau stulpelis 'key' nesikartoja (stulpeliai pervadinti, kad nesidubliuotų pavadinimai). Stulpelį 'key' teko nurodyti parametre on.

papildykime pavyzdį dar vienu stulpeliu:

key2 = 'B C D E F G'.split()
data_main['key2'] = key2
data_right['key2'] = key2
/usr/lib/python3/dist-packages/ipykernel_launcher.py:2: SettingWithCopyWarning: 
A value is trying to be set on a copy of a slice from a DataFrame.
Try using .loc[row_indexer,col_indexer] = value instead

See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
  
tai ne klaida, tai perspėjimas, ignoruokite. čia tiesiog greituoju būdu sukurta dummy data

data_main
Šalis	Miestas	Gyv	key	key2
0	Lietuva	Vilnius	541	A	B
1	Lietuva	Kaunas	287	B	C
2	Lietuva	Klaipėda	147	C	D
3	Latvija	Ryga	716	D	E
4	Latvija	Ventspilis	43	E	F
5	Latvija	Daugpilis	105	F	G
data_right
Šalis	Miestas	Gyv	key	key2
0	Estija	Talinas	400	A	B
1	Estija	Tartu	101	B	C
2	Estija	Pernu	46	C	D
3	Lenkija	Varšuva	1688	D	E
4	Lenkija	Vroclavas	638	E	F
5	Lenkija	Gdanskas	461	F	G
pd.merge(data_main, data_right, on=['key', 'key2'])
Šalis_x	Miestas_x	Gyv_x	key	key2	Šalis_y	Miestas_y	Gyv_y
0	Lietuva	Vilnius	541	A	B	Estija	Talinas	400
1	Lietuva	Kaunas	287	B	C	Estija	Tartu	101
2	Lietuva	Klaipėda	147	C	D	Estija	Pernu	46
3	Latvija	Ryga	716	D	E	Lenkija	Varšuva	1688
4	Latvija	Ventspilis	43	E	F	Lenkija	Vroclavas	638
5	Latvija	Daugpilis	105	F	G	Lenkija	Gdanskas	461
Matome, kad į parametrą on galima perduoti ir daugiau reikšmių, sąraše.

Jeigu, pvz. stulpelis 'key2' vienoje lentelėje skiriasi nuo kitos lentelės 'key2' stulpelio:

keyX = 'W C D E F W'.split()
data_right['key2'] = keyX
data_right
Šalis	Miestas	Gyv	key	key2
0	Estija	Talinas	400	A	W
1	Estija	Tartu	101	B	C
2	Estija	Pernu	46	C	D
3	Lenkija	Varšuva	1688	D	E
4	Lenkija	Vroclavas	638	E	F
5	Lenkija	Gdanskas	461	F	W
pd.merge(data_main, data_right, on=['key', 'key2'])
Šalis_x	Miestas_x	Gyv_x	key	key2	Šalis_y	Miestas_y	Gyv_y
0	Lietuva	Kaunas	287	B	C	Estija	Tartu	101
1	Lietuva	Klaipėda	147	C	D	Estija	Pernu	46
2	Latvija	Ryga	716	D	E	Lenkija	Varšuva	1688
3	Latvija	Ventspilis	43	E	F	Lenkija	Vroclavas	638
...gauname tik tas eilutes, kuriose 'key2' reikšmių sekos dalis sutampa.

Yra ir metodas .join(). Jis daro tą patį, ką ir merge, tik indekso pagrindu. Pvz.:

data_main.join(data_right, lsuffix='L', rsuffix='R')
ŠalisL	MiestasL	GyvL	keyL	key2L	ŠalisR	MiestasR	GyvR	keyR	key2R
0	Lietuva	Vilnius	541	A	B	Estija	Talinas	400	A	W
1	Lietuva	Kaunas	287	B	C	Estija	Tartu	101	B	C
2	Lietuva	Klaipėda	147	C	D	Estija	Pernu	46	C	D
3	Latvija	Ryga	716	D	E	Lenkija	Varšuva	1688	D	E
4	Latvija	Ventspilis	43	E	F	Lenkija	Vroclavas	638	E	F
5	Latvija	Daugpilis	105	F	G	Lenkija	Gdanskas	461	F	W
Kadangi sutampa stulpelių pavadinimai, teko nurodyti lsuffix ir rsuffix. Jeigu indeksas nebūtų identiškas, rezultate gautumėm tik tas eilutes, kurių indeksas persidengia. Dažniausiai vis tik naudosime .merge()
