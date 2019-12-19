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

4
```python
def read_in_lines(filename):
    with open(filename, 'r', encoding="utf-8") as file:
        line = 1
        while True:
            data = file.readlines(line)
            # Čia galima užsiimti text formatavimu, bet nebūtina.
            if not data:
                break
            yield data
            line += 1


generator = read_in_lines('os.py')
```