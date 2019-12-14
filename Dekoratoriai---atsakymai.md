Dekoratorių užduočių atsakymai:

1
```python
def args_limiter(fn):
    def wrapper(*args, **kwargs):
        if len(args) > 2:
            return "Too many arguments!"
        return fn(*args, **kwargs)
    return wrapper
```
2
```python
def string_args_only(fn):
    def wrapper(*args, **kwargs):
        for i in args:
            if type(i) != str:
                return "All args must be of type string!"
        return fn(*args, **kwargs)
    return wrapper
```

3 (visa programa):

```python
from functools import wraps
from time import time
import requests


def speed_test(fn):
    wraps(fn)
    def wrapper(*args, **kwargs):
        start_time = time()
        fn(*args, **kwargs)
        end_time = time()
        runtime = end_time - start_time
        print(f"Function's '{fn.__name__}', with given parameters {args} runtime: {round(runtime, 2)}s")
    return wrapper


@speed_test
def get_status(website):
    r = requests.get(website)
    print(r.status_code)


get_status('http://python.org')
```