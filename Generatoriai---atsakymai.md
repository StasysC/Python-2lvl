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
PIN = '0012'

def pin_breaker():
    num = 0
    while num < 10000:
        guess = f'{num:04}'
        if guess == PIN:
            print(f"{guess} That's your PIN!")
            break
        yield guess
        num += 1

gen = pin_breaker()

while True:
    try:
        print(next(gen))
    except StopIteration:
        break
```

Alternatyva 2:

```python
counter = (f"{num:04}" for num in range(10000))
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