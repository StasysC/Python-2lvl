NumPy yra tiesinės algebros biblioteka. Jos pagrindu sukurtos beveik visos su duomenų mokslu susijusios bibliotekos, tokios kaip Pandas ir kt. Numpy yra itin greita, nes yra susieta ryšiais(bindings) su C kalba parašytais moduliais.
Standartiškai įsidiegia pip install numpy, jeigu naudojate Anaconda - conda install numpy.

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

#[[1, 2, 3],
# [4, 5, 6],
# [7, 8, 9]]
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
jeigu matricos iš nulių:

np.zeros((5,5))
#[[0. 0. 0. 0. 0.]
# [0. 0. 0. 0. 0.]
# [0. 0. 0. 0. 0.]
# [0. 0. 0. 0. 0.]
# [0. 0. 0. 0. 0.]]
```
Analogiškai veikia np.ones metodas. Dar viena naudinga funkcija - linspace. Ji grąžina masyvą, su lygiais intervalais išdėliotomis reikšmėmis. Reikia nurodyti start, stop ir intervalo reikšmes:
```python
np.linspace(0,20,16)
#[ 0.          1.33333333  2.66666667  4.          5.33333333  6.66666667
#  8.          9.33333333 10.66666667 12.         13.33333333 14.66666667
# 16.         17.33333333 18.66666667 20.        ]
```
Jeigu prireikė vienetinės matricos:
```python
np.eye(6)
#[[1. 0. 0. 0. 0. 0.]
# [0. 1. 0. 0. 0. 0.]
# [0. 0. 1. 0. 0. 0.]
# [0. 0. 0. 1. 0. 0.]
# [0. 0. 0. 0. 1. 0.]
# [0. 0. 0. 0. 0. 1.]]
```
## Random arrays kūrimas
Pirmas metodas susikurti random array - np.random.rand(). Jo pagalba galime susikurti masyvą su atsitiktinėm reikšmėm nuo 0 iki 1 ("uniform" distribution)

np.random.rand(10)
array([0.05354825, 0.71622013, 0.03802812, 0.80017304, 0.79186933,
       0.14834037, 0.11068095, 0.39367325, 0.67202456, 0.11014383])
jeigu norime ne vektoriaus, o matricos:

np.random.rand(5,5)
array([[0.74749758, 0.03612215, 0.57549452, 0.40745415, 0.54612509],
       [0.08944715, 0.97328185, 0.75301528, 0.06295328, 0.70474664],
       [0.62781843, 0.5696614 , 0.37032677, 0.17572604, 0.35318   ],
       [0.96385854, 0.96901831, 0.36965118, 0.20354899, 0.24901119],
       [0.44060767, 0.11242012, 0.66194733, 0.73046754, 0.46718651]])
np.random.randn() sugeneruos reikšmes iš “standard normal” distribution (standartinis normalusis skirstinys)

np.random.randn(3,3)
array([[ 1.65025793,  1.77855175, -0.7092368 ],
       [-1.06461994, -1.83109209, -0.37089846],
       [-0.28549594, -0.35227789, -1.64371272]])
np.random.randint() sugeneruoja atsitiktines integer reikšmes. Parametruose reikia nurodyti, žemiausią, aukščiausią (neįskaitant) reikšmes ir norimą kiekį reikšmių.

np.random.randint(100, 200, 20)
array([148, 139, 183, 108, 177, 177, 188, 176, 178, 103, 123, 140, 189,
       170, 152, 162, 146, 185, 128, 100])
Masyvų pertvarkymas
reshape() metodas leidžia mums performuoti turimą masyvą į kitą formą:

my_array = np.random.randint(0, 100, 64)
my_array
array([15, 54, 20, 25, 34, 14, 93, 81, 20, 12,  9,  3,  7, 14, 32, 46, 38,
        1, 74, 67, 31, 88, 87, 36, 22, 53, 93, 52, 10, 31, 51, 89, 78,  8,
       26, 32, 38, 77, 28, 48, 87, 94,  1, 10, 75, 50,  0, 79, 28, 81, 68,
       53, 87, 83, 10, 75, 41,  2, 44, 24,  7, 94, 38, 49])
reshaped_array = my_array.reshape(8,8)
reshaped_array
array([[15, 54, 20, 25, 34, 14, 93, 81],
       [20, 12,  9,  3,  7, 14, 32, 46],
       [38,  1, 74, 67, 31, 88, 87, 36],
       [22, 53, 93, 52, 10, 31, 51, 89],
       [78,  8, 26, 32, 38, 77, 28, 48],
       [87, 94,  1, 10, 75, 50,  0, 79],
       [28, 81, 68, 53, 87, 83, 10, 75],
       [41,  2, 44, 24,  7, 94, 38, 49]])
šiame pavyzdyje vektorių iš 64 reikšmių performavome į 8x8 matricą.

Naudingi Metodai
max() ir .min() metodai ištraukia maksimalią ir minimalią reikšmes iš masyvo:

my_array.min()
0
my_array.max()
94
argmax() ir argmin() nurodo mums maksimalios ir minimalios reikšmių indeksą:

my_array.argmax()
41
my_array.argmin()
46
.shape nurodo, kokią formą turi mūsų masyvas:

reshaped_array.shape
(8, 8)
.dtype nurodo, koks duomenų tipas yra mūsų masyve:

reshaped_array.dtype
dtype('int64')
Indeksacija ir reikšmių traukimas
sample_array = np.arange(1,10)
sample_array
array([1, 2, 3, 4, 5, 6, 7, 8, 9])
reikšmę iš vektoriaus traukiame taip pat kaip ir iš Python sąrašo:

sample_array[5]
6
galime naudoti slices:

sample_array[2:8]
array([3, 4, 5, 6, 7, 8])
sample_array[6:]
array([7, 8, 9])
sample_array[-5:]
array([5, 6, 7, 8, 9])
galime pasirinktam rėžiui suteikti kokią nors savo reikšmę (Broadcasting):

sample_array[4:8] = 50
sample_array
array([ 1,  2,  3,  4, 50, 50, 50, 50,  9])
Reikšmių traukimas iš matricos
sample = np.random.randint(1, 10, 25)
sample_matrix = sample.reshape(5,5)
sample_matrix
array([[8, 9, 8, 7, 3],
       [8, 5, 2, 4, 2],
       [1, 4, 6, 1, 6],
       [8, 2, 3, 8, 7],
       [2, 6, 6, 1, 8]])
sample_matrix[2,2] 
6
laužtiniuose skliausteliuose pirmiau nurodome eilutę, paskui tos eilutės nario indeksą.

taip pat galime naudoti rėžius:

sample_matrix[1:4, 1:4]
array([[5, 2, 4],
       [4, 6, 1],
       [2, 3, 8]])
sample_matrix[3:,:]
array([[8, 2, 3, 8, 7],
       [2, 6, 6, 1, 8]])
sample_matrix[:, 0:2]
array([[8, 9],
       [8, 5],
       [1, 4],
       [8, 2],
       [2, 6]])
Reikšmių traukimas pagal sąlygą
Tarkime, turime masyvą:

masyvas = np.arange(1,21)
masyvas
array([ 1,  2,  3,  4,  5,  6,  7,  8,  9, 10, 11, 12, 13, 14, 15, 16, 17,
       18, 19, 20])
norime reikšmių, didesnių už 9:

bool_masyvas = masyvas > 9
bool_masyvas
array([False, False, False, False, False, False, False, False, False,
        True,  True,  True,  True,  True,  True,  True,  True,  True,
        True,  True])
gauname masyvą iš bool reikšmių, kuriame True reikšmės atitinka užduotą sąlygą. Atlikime tokią operaciją:

masyvas[bool_masyvas]
array([10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20])
kintamojo masvas laužtiniuose skliautuose įvedę kintamąjį bool_masyvas, gauname reikšmes, kurios atitinka True indeksą. Tą patį rezultatą galime gauti laužtiniuose skliaustuose tiesiog įrašę sąlygą:

masyvas[masyvas>9]
array([10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20])
Numpy elgsenos ypatumai
Yra tam tikri NumPy elgsenos ypatumai, tarkime:

pvz = np.random.randint(1, 21, 20)
pvz
array([11, 18, 13,  2, 11, 10,  3, 11, 15,  1,  3, 11, 12,  7, 16, 19,  6,
       20,  1, 19])
turime random masyvą iš integer reikšmių. Susikurkime jo atraižą:

pvz_ispjova = pvz[5:15]
pvz_ispjova
array([10,  3, 11, 15,  1,  3, 11, 12,  7, 16])
pvz_ispjova[:] = 99
pvz_ispjova
array([99, 99, 99, 99, 99, 99, 99, 99, 99, 99])
Iki šio momento viskas atrodo kaip ir tikėtąsi. Tačiau išsikvietę pirmąjį masyvą matome:

pvz
array([11, 18, 13,  2, 11, 99, 99, 99, 99, 99, 99, 99, 99, 99, 99, 19,  6,
       20,  1, 19])
Paprastai kuriant kintamąjį, užkulisiuose padaroma kopija šaltinio, iš kurio jis gaminamas (šiuo atveju pvz). Iš tos kopijos formuojamas naujas kintamasis. Tačiau NumPy atveju pakeitimai vykdomi originale, ir mums rodoma tik modifikuota to originalo dalis. NumPy pritaikytas darbui su milžiniškais kiekiais duomenų. Daryti laikinas jų kopijas atmintyje yra neefektyvu, ir nestabilu. Todėl, kai norime išsaugoti originalą, turime nurodyti, kad norėsime pasidaryti kopiją:

pvz_copy = pvz.copy()
pvz_copy
array([11, 18, 13,  2, 11, 99, 99, 99, 99, 99, 99, 99, 99, 99, 99, 19,  6,
       20,  1, 19])
pvz_copy == pvz
array([ True,  True,  True,  True,  True,  True,  True,  True,  True,
        True,  True,  True,  True,  True,  True,  True,  True,  True,
        True,  True])
pvz_copy_ispjova = pvz_copy[5:15]
pvz_copy_ispjova[:] = 100
pvz_copy_ispjova
array([100, 100, 100, 100, 100, 100, 100, 100, 100, 100])
pvz
array([11, 18, 13,  2, 11, 99, 99, 99, 99, 99, 99, 99, 99, 99, 99, 19,  6,
       20,  1, 19])
pvz_copy
array([ 11,  18,  13,   2,  11, 100, 100, 100, 100, 100, 100, 100, 100,
       100, 100,  19,   6,  20,   1,  19])
Taigi, pasidarėme kopiją, nurodėme kad norime jos rėžio [5:15] kintamąjame pvz_copy_ispjova, joje visas reikšmes pakeitėme į 100, ir įsitikinome, kad po to originalusis pvz liko nepakeistas.

Matematinės operacijos ir funkcijos
su NumPy arrays galima atlikti paprastus aritmetinius veiksmus:

vektorius = np.arange(1,11)
vektorius
array([ 1,  2,  3,  4,  5,  6,  7,  8,  9, 10])
vektorius + vektorius
array([ 2,  4,  6,  8, 10, 12, 14, 16, 18, 20])
vektorius * vektorius
array([  1,   4,   9,  16,  25,  36,  49,  64,  81, 100])
vektorius / vektorius
array([1., 1., 1., 1., 1., 1., 1., 1., 1., 1.])
vektorius / 0
/home/robotautas/anaconda3/lib/python3.7/site-packages/ipykernel_launcher.py:1: RuntimeWarning: divide by zero encountered in true_divide
  """Entry point for launching an IPython kernel.
array([inf, inf, inf, inf, inf, inf, inf, inf, inf, inf])
atkreipkite dėmesį, atlikus dalybą iš 0 gausime begalybes arba nan - not a number. Taip pat galime atlikti veiksmus ir su skaičiais:

vektorius + 1000
array([1001, 1002, 1003, 1004, 1005, 1006, 1007, 1008, 1009, 1010])
vektorius ** 3
array([   1,    8,   27,   64,  125,  216,  343,  512,  729, 1000])
ir t.t.

Numpy aplinkoje taip pat galime taikyti įvairias trigonometrines funkcijas ir tt.

np.sin(vektorius)
array([ 0.84147098,  0.90929743,  0.14112001, -0.7568025 , -0.95892427,
       -0.2794155 ,  0.6569866 ,  0.98935825,  0.41211849, -0.54402111])
np.log(vektorius)
array([0.        , 0.69314718, 1.09861229, 1.38629436, 1.60943791,
       1.79175947, 1.94591015, 2.07944154, 2.19722458, 2.30258509])
Visas matematines funkcijas galite surasti čia.
