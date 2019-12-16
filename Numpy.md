
# NumPy

* NumPy yra tiesinės algebros biblioteka. Jos pagrindu sukurtos beveik visos su duomenų mokslu susijusios bibliotekos, tokios kaip Pandas ir kt. Numpy yra itin greita, nes yra susieta ryšiais(bindings) su C kalba parašytais moduliais. 

* Standartiškai įsidiegia *pip install numpy*, jeigu naudojate Anaconda - *conda install numpy*
* Dažniausiai naudojamas NumPy ingredientas - NumPy masyvai. Jie būna dviejų tipų - vektoriai ir matricos.  

Prieš pradedant darbą su NumPy, reikia jį importuoti.


```python
import numpy as np
```

tarkime, turime paprastą Python list'ą:


```python
listas = [1, 2, 3, 4, 5]
```

paveskime jį į NumPy array:


```python
arr = np.array(listas)
```


```python
arr
```




    array([1, 2, 3, 4, 5])



gauname 1 lygio NumPy masyvą (vektorių). Jeigu norime matricos, turime sukurti keletą masyvų masyve:


```python
mano_listai = [[1, 2, 3],[4, 5, 6],[7, 8, 9]]
matrica = np.array(mano_listai)

```


```python
matrica
```




    array([[1, 2, 3],
           [4, 5, 6],
           [7, 8, 9]])



NumPy turi ir integruotus, paprastus būdus susikurti masyvą. Skliausteliuose reikia įrašyti start, stop ir step(nebūtina) reikšmes:


```python
np.arange(0,30,3)
```




    array([ 0,  3,  6,  9, 12, 15, 18, 21, 24, 27])



jeigu reikia vektoriaus iš nulių:


```python
np.zeros(10)
```




    array([0., 0., 0., 0., 0., 0., 0., 0., 0., 0.])



jeigu matricos iš nulių:


```python
np.zeros((5,5))
```




    array([[0., 0., 0., 0., 0.],
           [0., 0., 0., 0., 0.],
           [0., 0., 0., 0., 0.],
           [0., 0., 0., 0., 0.],
           [0., 0., 0., 0., 0.]])



Analogiškai veikia np.ones metodas.
Dar viena naudinga funkcija - linspace. Ji grąžina masyvą, su lygiais intervalais išdėliotomis reikšmėmis. Reikia nurodyti start, stop ir intervalo reikšmes:


```python
np.linspace(0,20,16)
```




    array([ 0.        ,  1.33333333,  2.66666667,  4.        ,  5.33333333,
            6.66666667,  8.        ,  9.33333333, 10.66666667, 12.        ,
           13.33333333, 14.66666667, 16.        , 17.33333333, 18.66666667,
           20.        ])



Jeigu prireikė vienetinės matricos:


```python
np.eye(6)
```




    array([[1., 0., 0., 0., 0., 0.],
           [0., 1., 0., 0., 0., 0.],
           [0., 0., 1., 0., 0., 0.],
           [0., 0., 0., 1., 0., 0.],
           [0., 0., 0., 0., 1., 0.],
           [0., 0., 0., 0., 0., 1.]])




```python

```