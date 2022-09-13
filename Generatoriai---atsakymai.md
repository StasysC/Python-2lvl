1
```python
def poriniai():
    number = 2
    while True:
        yield number
        number += 2
```

2
```python
def fibonacci():
    a, b = 0, 1
    while True:
        yield a
        a, b = b, a + b
```

3
```python
#Tarkime, kad teisingas pin yra 0123
PIN = '0123'

def pin_breaker():
    guess = 0
    while True:
        yield guess
        if guess == int(PIN):
            if len(str(guess)) < 4:
                if len(str(guess)) == 3:
                    print(f'PIN is 0{guess}!')
                elif len(str(guess)) == 2:
                    print(f'PIN is 00{guess}!')
                else:
                    print(f'PIN is 000{guess}!')
            else:
                print(f'PIN is {guess}!')
            break
        guess += 1


generator = pin_breaker()
for num in generator:
    #Čia irgi galime įterpti logiką, kad spausdintų nulius prieky
    print(num)
```

Alternatyva:


```python
#Tarkime, kad teisingas pin yra 0123
PIN = '9999'

def pin_breaker(pin):
    guess = 0
    while True:
        res = ("0" * (4 - (len(str(guess))))) + str(guess)
        if res == pin:
            print(f"PIN is {res}")
            break
        yield res
        guess += 1


generator = pin_breaker(PIN)
for num in generator:
    #Čia irgi galime įterpti logiką, kad spausdintų nulius prieky
    print(num)
```

Alternatyva 2:

```python
counter = ("%.4d" % num for num in range(10000))
pin_list = list(counter)
for pin in pin_list:
    print(pin)
    if pin == "0549":
        print(f"PIN kodas yra: {pin}")
        break
```

4
```python
def read_in_lines(filename):
    with open(filename, 'r', encoding="utf-8") as file:
        for line in file:
            yield line[:-1]


generator = read_in_lines('tekstas.txt')

for x in generator:
    print(x)

```