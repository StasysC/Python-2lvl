NumPy yra tiesinės algebros biblioteka. Jos pagrindu sukurtos beveik visos su duomenų mokslu susijusios bibliotekos, tokios kaip Pandas ir kt. Numpy yra itin greita, nes yra susieta ryšiais(bindings) su C kalba parašytais moduliais.
Standartiškai įsidiegia pip install numpy.

## Vektoriai
Dažniausiai naudojamas NumPy ingredientas - NumPy masyvai. Jie būna dviejų tipų - vektoriai ir matricos.
Prieš pradedant darbą su NumPy, reikia jį importuoti.
```python
import numpy as np
tarkime, turime paprastą Python list'ą:
```
```python
listas = [1, 2, 3, 4, 5]
```
paveskime jį į NumPy array:
```python
arr = np.array(listas)
# [1 2 3 4 5]
```
gauname 1 lygio NumPy masyvą (vektorių).
## Matricos
Jeigu norime matricos, turime sukurti keletą masyvų masyve:
```python
mano_listai = [[1, 2, 3],[4, 5, 6],[7, 8, 9]]
matrica = np.array(mano_listai)

# [[1, 2, 3],
#  [4, 5, 6],
#  [7, 8, 9]]
```
## NumPy built-in funkcionalumas
NumPy turi ir integruotus, paprastus būdus susikurti masyvą. Skliausteliuose reikia įrašyti start, stop ir step(nebūtina) reikšmes:
```python
np.arange(0,30,3)

# [ 0  3  6  9 12 15 18 21 24 27]
```
jeigu reikia vektoriaus iš nulių:
```python
np.zeros(10)

# [0. 0. 0. 0. 0. 0. 0. 0. 0. 0.]
```
jeigu matricos iš nulių:
```python
np.zeros((5,5))

# [[0. 0. 0. 0. 0.]
#  [0. 0. 0. 0. 0.]
#  [0. 0. 0. 0. 0.]
#  [0. 0. 0. 0. 0.]
#  [0. 0. 0. 0. 0.]]
```
Analogiškai veikia np.ones metodas. Dar viena naudinga funkcija - linspace. Ji grąžina masyvą, su lygiais intervalais išdėliotomis reikšmėmis. Reikia nurodyti start, stop ir intervalo reikšmes:
```python
np.linspace(0,20,16)

# [ 0.          1.33333333  2.66666667  4.          5.33333333  6.66666667
#   8.          9.33333333 10.66666667 12.         13.33333333 14.66666667
#   16.         17.33333333 18.66666667 20.        ]
```
Jeigu prireikė vienetinės matricos:
```python
np.eye(6)

# [[1. 0. 0. 0. 0. 0.]
#  [0. 1. 0. 0. 0. 0.]
#  [0. 0. 1. 0. 0. 0.]
#  [0. 0. 0. 1. 0. 0.]
#  [0. 0. 0. 0. 1. 0.]
#  [0. 0. 0. 0. 0. 1.]]
```
## Random arrays kūrimas
Pirmas metodas susikurti random array - np.random.rand(). Jo pagalba galime susikurti masyvą su atsitiktinėm reikšmėm nuo 0 iki 1 ("uniform" distribution)
```python
np.random.rand(10)

# [0.2428621  0.12122176 0.03113639 0.61134008 0.55336052 0.39831215
#  0.21657977 0.0346176  0.77559089 0.42822333]
```
jeigu norime ne vektoriaus, o matricos:
```python
np.random.rand(5,5)

# [[0.77635924 0.63103075 0.53459308 0.21713619 0.37158872]
#  [0.37068294 0.62333135 0.4164486  0.85398205 0.7266794 ]
#  [0.89177106 0.41142509 0.2933069  0.42827223 0.34496961]
#  [0.88389908 0.15904759 0.11562505 0.23804093 0.99464436]
#  [0.64899248 0.73697882 0.13380731 0.09794041 0.91591006]]
```
**np.random.randn()** sugeneruos reikšmes iš “standard normal” distribution (standartinis normalusis skirstinys)
```python
np.random.randn(3,3)

# [[ 1.21300788 -0.35299473 -1.14654566]
#  [-1.20397401 -0.11634871  1.23841237]
#  [ 0.54530069 -1.93170697  0.09167598]]
```
**np.random.randint()** sugeneruoja atsitiktines integer reikšmes. Parametruose reikia nurodyti, žemiausią, aukščiausią (neįskaitant) reikšmes ir norimą kiekį reikšmių.
```python
np.random.randint(100, 200, 20)

# [127 137 128 164 115 153 109 122 137 199 136 115 107 114 160 126 168 129
#  135 109]
```
## Masyvų pertvarkymas
**reshape()** metodas leidžia mums performuoti turimą masyvą į kitą formą:
```python
my_array = np.random.randint(0, 100, 64)

# [99 78 61 16 73  8 62 27 30 80  7 76 15 53 80 27 44 77 75 65 47 30 84 86
#  18  9 41 62  1 82 16 78  5 58  0 80  4 36 51 27 31  2 68 38 83 19 18  7
#  30 62 11 67 65 55  3 91 78 27 29 33 89 85  7 16]
```
```python
reshaped_array = my_array.reshape(8,8)

# [[99 78 61 16 73  8 62 27]
#  [30 80  7 76 15 53 80 27]
#  [44 77 75 65 47 30 84 86]
#  [18  9 41 62  1 82 16 78]
#  [ 5 58  0 80  4 36 51 27]
#  [31  2 68 38 83 19 18  7]
#  [30 62 11 67 65 55  3 91]
#  [78 27 29 33 89 85  7 16]]
```
šiame pavyzdyje vektorių iš 64 reikšmių performavome į 8x8 matricą.

## Naudingi Metodai
**max()** ir **min()** metodai ištraukia maksimalią ir minimalią reikšmes iš masyvo:
```python
my_array.min()
my_array.max()
```
**argmax()** ir **argmin()** nurodo mums maksimalios ir minimalios reikšmių indeksą:
```python
my_array.argmax()
my_array.argmin()
```
**.shape** nurodo, kokią formą turi mūsų masyvas:
```python
reshaped_array.shape

# (8, 8)
```
**.dtype** nurodo, koks duomenų tipas yra mūsų masyve:
```python
reshaped_array.dtype

# int32
```
## Indeksacija ir reikšmių traukimas
```python
sample_array = np.arange(1,10)

# [1 2 3 4 5 6 7 8 9]
```
reikšmę iš vektoriaus traukiame taip pat kaip ir iš Python sąrašo:
```python
sample_array[5]
# 6
```
galime naudoti slices:
```python
sample_array[2:8]

# [3 4 5 6 7 8]

sample_array[6:]

# [7 8 9]

sample_array[-5:]

# [5 6 7 8 9]
```
galime pasirinktam rėžiui suteikti kokią nors savo reikšmę (Broadcasting):
```python
sample_array[4:8] = 50

# [ 1  2  3  4 50 50 50 50  9]

## Reikšmių traukimas iš matricos
```python
sample = np.random.randint(1, 10, 25)
sample_matrix = sample.reshape(5,5)

# [[4 7 7 1 9]
#  [5 8 1 1 8]
#  [2 6 8 1 2]
#  [5 7 3 2 3]
#  [8 1 6 1 1]]

sample_matrix[2,2] 

# 6
```
laužtiniuose skliausteliuose pirmiau nurodome eilutę, paskui tos eilutės nario indeksą.

taip pat galime naudoti rėžius:
```python
sample_matrix[1:4, 1:4]

# [[8 1 1]
#  [6 8 1]
#  [7 3 2]]

sample_matrix[3:, :]

# [[5 7 3 2 3]
#  [8 1 6 1 1]]

sample_matrix[:, 0:2]

# [[4 7]
#  [5 8]
#  [2 6]
#  [5 7]
#  [8 1]]
```
## Reikšmių traukimas pagal sąlygą
Tarkime, turime masyvą:
```python
masyvas = np.arange(1,21)

# [ 1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20]
```
norime reikšmių, didesnių už 9:
```python
bool_masyvas = masyvas > 9
bool_masyvas
# [False False False False False False False False False  True  True  True
#   True  True  True  True  True  True  True  True]
```
gauname masyvą iš bool reikšmių, kuriame True reikšmės atitinka užduotą sąlygą. Atlikime tokią operaciją:
```python
masyvas[bool_masyvas]

# [10 11 12 13 14 15 16 17 18 19 20]
```
kintamojo masyvo laužtiniuose skliautuose įvedę kintamąjį bool_masyvas, gauname reikšmes, kurios atitinka True indeksą. Tą patį rezultatą galime gauti laužtiniuose skliaustuose tiesiog įrašę sąlygą:
```python
masyvas[masyvas>9]

# [10 11 12 13 14 15 16 17 18 19 20]
```
## Numpy elgsenos ypatumai
Yra tam tikri NumPy elgsenos ypatumai, tarkime:
```python
pvz = np.random.randint(1, 21, 20)

# [ 4 15 16  7 17 10  9  5  8 17 17  8 13 16 18  8 17 13 14 12]
```
turime random masyvą iš integer reikšmių. Susikurkime jo atraižą:
```python
pvz_ispjova = pvz[5:15]

# [10  9  5  8 17 17  8 13 16 18]

pvz_ispjova[:] = 99

#[99 99 99 99 99 99 99 99 99 99]
```
Iki šio momento viskas atrodo kaip ir tikėtąsi. Tačiau išsikvietę pirmąjį masyvą matome:
```python
print(pvz)

# [ 4 15 16  7 17 99 99 99 99 99 99 99 99 99 99  8 17 13 14 12]
```
Paprastai kuriant kintamąjį, užkulisiuose padaroma kopija šaltinio, iš kurio jis gaminamas (šiuo atveju pvz). Iš tos kopijos formuojamas naujas kintamasis. Tačiau NumPy atveju pakeitimai vykdomi originale, ir mums rodoma tik modifikuota to originalo dalis. NumPy pritaikytas darbui su milžiniškais kiekiais duomenų. Daryti laikinas jų kopijas atmintyje yra neefektyvu, ir nestabilu. Todėl, kai norime išsaugoti originalą, turime nurodyti, kad norėsime pasidaryti kopiją:
```python
pvz_copy = pvz.copy()

# [ 4 15 16  7 17 99 99 99 99 99 99 99 99 99 99  8 17 13 14 12]

pvz_copy_ispjova = pvz_copy[5:15]
pvz_copy_ispjova[:] = 100

# [  4  15  16   7  17 100 100 100 100 100 100 100 100 100 100   8  17  13
  14  12]

print(pvz)
# [ 4 15 16  7 17 10  9  5  8 17 17  8 13 16 18  8 17 13 14 12]
```
Taigi, pasidarėme kopiją, nurodėme kad norime jos rėžio [5:15] kintamąjame pvz_copy_ispjova, joje visas reikšmes pakeitėme į 100, ir įsitikinome, kad po to originalusis pvz liko nepakeistas.

## Matematinės operacijos ir funkcijos
Su NumPy arrays galima atlikti paprastus aritmetinius veiksmus:
```python
vektorius = np.arange(1,11)

# [ 1  2  3  4  5  6  7  8  9 10]

vektorius + vektorius

# [ 2  4  6  8 10 12 14 16 18 20]

vektorius * vektorius

# [  1   4   9  16  25  36  49  64  81 100]

vektorius / vektorius

# [1. 1. 1. 1. 1. 1. 1. 1. 1. 1.]

vektorius / 0

# [inf inf inf inf inf inf inf inf inf inf]
C:\Users\scivi\PycharmProjects\PTU21\main.py:3: RuntimeWarning: divide by zero encountered in divide
  print(vektorius / 0)
```
atkreipkite dėmesį, atlikus dalybą iš 0 gausime begalybes arba nan - not a number. Taip pat galime atlikti veiksmus ir su skaičiais:
```python
vektorius + 1000

# [101 102 103 104 105 106 107 108 109 110]

vektorius ** 3

# [   1    8   27   64  125  216  343  512  729 1000]
```
ir t.t.

Numpy aplinkoje taip pat galime taikyti įvairias trigonometrines funkcijas ir tt.
```python
np.sin(vektorius)

# [ 0.84147098  0.90929743  0.14112001 -0.7568025  -0.95892427 -0.2794155
#   0.6569866   0.98935825  0.41211849 -0.54402111]

np.log(vektorius)

# [0.         0.69314718 1.09861229 1.38629436 1.60943791 1.79175947
#  1.94591015 2.07944154 2.19722458 2.30258509]
```
Visas matematines funkcijas galite surasti [čia](https://numpy.org/doc/stable/reference/ufuncs.html).

# Užduotys
## 1 užduotis
Išbandykite NumPy funkcionalumą ir atlikite šiuos veiksmus:
* Sukurkite vektorių su skaičiais nuo 1 iki 9
* Sukurkite vektorių iš 10 nulių
* Sukurkite vektorių iš 10 vienetų
* Sukurkite vektorių iš 10 ketvertų
* Sukurkite vektorių iš lyginių skaičių nuo 0 iki 100

## 2 užduotis
Atlikitie veiksmus su skaičių matrica:
* Sukurkite matricą iš 25 narių, pradedant 1, baigiant 25. Priskirkite ją kintamąjam.
* Iš anksčiau sukurtos matricos ištraukite skaičių 12
* Iš anksčiau sukurtos matricos ištraukite paskutinę eilutę.
* Iš anksčiau sukurtos matricos ištraukite submatricą:
```python
[[1 2 3]
 [6 7 8]
 [11 12 13]]
```
* Iš anksčiau sukurtos matricos ištraukite submatricą:
```python
[[7 8 9 10]
 [12 13 14 15]
 [17 18 19 20]] 
```
* Iš anksčiau sukurtos matricos ištraukite submatricą
```python
[[16 17 18]
 [21 22 23]]
```
## 3 užduotis

Sukurkite vektorių iš 20 atsitiktinių reikšmių nuo 0 iki 1. Priskirkite kintamąjam, tada atlikite šiuos veiksmus:
* Suraskite didžiausią reikšmę masyve ir jos indeksą.
* Suraskite mažiausią reikšmę ir jos indeksą
* Atspausdinkite šio vektoriaus duomenų tipą

## 4 užduotis

Sukurkite vektorių iš integer reikšmių nuo 1 iki 100. Priskirkite kintamąjam ir atlikite šiuos veiksmus:
* Iš jo ištraukite visus skaičius, didesnius už 90
* Iš pradinio vektoriaus ištraukite visus skaičiaus 7 kartotinius

## 5 užduotis
Sukurkite tokią matricą:
```python
[[0.025 0.05 0.075 0.1 0.125 0.15 0.175 0.2],
 [0.225 0.25 0.275 0.3 0.325 0.35 0.375 0.4],
 [0.425 0.45 0.475 0.5 0.525 0.55 0.575 0.6],
 [0.625 0.65 0.675 0.7 0.725 0.75 0.775 0.8],
 [0.825 0.85 0.875 0.9 0.925 0.95 0.975 1.]])
```

Sukurkite tokią matricą (sveiki sk. nuo 2 iki 1000 iš kurių traukiasi sveika šaknis):
```python
[[  4   9  16  25  36],
 [ 49  64  81 100 121],
 [144 169 196 225 256],
 [289 324 361 400 441],
 [484 529 576 625 676],
 [729 784 841 900 961]])
```
## Papildoma užduotis

* Sukurkite vektorių iš sveikų sk. nuo 1 iki 100. Priskirkite kintamąjam.
* Sukurkite Python funkciją, kuri tikrina ar parametruose įvestas sk. yra pirminis. Jeigu pirminis, grąžina True, jei ne, False.
* NumPy nevisada supranta įprastą Python kodą su range'ais ir list'ais, todėl sukurtą funkciją teks vektorizuoti taip :
```python
  nauja_funkcija = np.vectorize(jūsų_funkcija) .
```
* Kadangi sąlygos reikšmių traukimui yra bool reikšmės, pabandykite vietoje sąlygos įdėti savo vektorizuotą funkciją, ir taip išrinkti pirminius skaičius iš savo vektoriaus .
