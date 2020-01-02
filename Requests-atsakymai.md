# 1
```python
import requests

def random_cat(quantity):
    for i in range(quantity):
        r = requests.get('https://cataas.com/cat')
        with open(f'cat{i}.jpg', 'wb') as file:
            file.write(r.content)
```

# 2
```python
def sites_headers_data(*args):
    print('URL\t\t\tServer')
    print('-------------------------------------')
    for site in args:
        r = requests.get(site)
        result = r.headers
        print(f'{r.url}\t{result["Server"]}')

sites_headers_data('http://delfi.lt', 'http://alfa.lt', 'http://15min.lt', 'http://lrytas.lt', 'http://google.com')
```