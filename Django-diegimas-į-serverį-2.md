# Apsaugome jautrius Django duomenis

### Sukuriame konfiguracinį json failą

```bash
vartotojas@ubuntu:~$ sudo touch /etc/config.json
```

Atsidarome sukurtą failą su nano:
```bash
vartotojas@ubuntu:~$ sudo nano /etc/config.json
```

Jame įrašome tuos duomenis, kurie neturėtų būti settings.py faile.
Šiuo atveju, SECRET_KEY, taip pat el. pašto adresą ir slaptažodį:

```json                                                                                           
{
    "SECRET_KEY": "s9n*x9ysrn@kz%rfu96$du%40gew8buq-fj3b1@=vgd-r-k06#",
    "EMAIL_HOST_USER": "jusuel@pastas.lt",                                                   
    "EMAIL_HOST_PASSWORD": "jusu_slaptazodis"                                       
}

```

### Išimame jautrius duomenis iš settings.py:

Atsidarome per open config failą:
```python
import json

with open ('/etc/config.json') as config_file:
    config = json.load(config_file) 
```

Nustatome SECRET_KEY nuskaitymą iš failo:
```python
SECRET_KEY = config['SECRET_KEY']
```

Nustatome el. pašto duomenų nuskaitymą iš failo:
```python
EMAIL_BACKEND = 'django.core.mail.backends.console.EmailBackend'
EMAIL_HOST = 'smtp.gmail.com'                                                               
EMAIL_POST = 587
EMAIL_USE_TLS = True
EMAIL_HOST_USER = config.get('EMAIL_HOST_USER')                                             
EMAIL_HOST_PASSWORD = config.get('EMAIL_HOST_PASSWORD')  
```

Perkrauname Apache2 serverį:
```bash
vartotojas@ubuntu:~$ sudo systemctl restart apache2
```

# Įkeliame ir atnaujiname projektą per GIT:

Ištriname seną projekto katalogą:
```bash
vartotojas@ubuntu:/var/www$ sudo rm -r mysite/
```