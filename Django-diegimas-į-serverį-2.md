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

Įdiegiame GIT:
```bash
vartotojas@ubuntu:/var/www$ sudo apt install git 
```

Ištriname seną projekto katalogą:
```bash
vartotojas@ubuntu:/var/www$ sudo rm -r mysite/
```

Klonuojame projekto GIT repozitoriją, pvz.:
```bash
vartotojas@ubuntu:/var/www$ git clone https://github.com/DonatasNoreika/django_tinklarastis.git  
```

# Aktyvuojame SSL(TLS) (HTTPS) sertifikatą

Atsidarome svetainę https://letsencrypt.org/, spaudžiame "Get Started" ir spaudžiame ant nuorodos "Certbot".
Šiame puslapyje pasirenkame savo serverio sistemą ir operacinę sistemą (mūsų atveju - Apache ir Ubuntu 20.04)

Prisijungiame prie mūsų serverio ir leidžiame šias komandas (jei komandos skiriasi, leiskime jas), pvz.:
```bash
vartotojas@ubuntu:~$ sudo apt-get update
vartotojas@ubuntu:~$ sudo apt-get install software-properties-common
vartotojas@ubuntu:~$ sudo add-apt-repository universe
vartotojas@ubuntu:~$ sudo apt-get update
vartotojas@ubuntu:~$ sudo apt-get install certbot python3-certbot-apache
```

Atsidarome mūsų Apache konfiguracinį failą:
```bash
vartotojas@ubuntu:~$ sudo nano /etc/apache2/sites-enabled/mysite.conf 
```

Užkomentuojame šias eilutes:
```
    #WSGIDaemonProcess mysite processes=1 threads=15 python-path=/var/w>    
    #WSGIProcessGroup mysite
    #WSGIScriptAlias / /var/www/mysite/mysite/wsgi.py
```

Dabar jau leidžiame:
```bash
vartotojas@ubuntu:~$ sudo certbot --apache
```
Nurodome savo el. pašto adresą, patvirtiname taisykles (A), leidžiame (arba ne) siųsti naujienas (N), pasirenkame savo puslapį (1) galiausiai pasirenkame 2 (Redirect, kad leistų tik https užklausas)

Atsidarome mūsų Apache konfiguracinį failą:
```bash
vartotojas@ubuntu:~$ sudo nano /etc/apache2/sites-enabled/mysite.conf 
```

ir matome, kad failo apačioje yra įrašytos trys eilutės:
```

```

Atsidarome mūsų naujai sukurtą konfiguracinį failą:
```bash
vartotojas@ubuntu:~$ sudo nano /etc/apache2/sites-enabled/mysite-le-ssl.conf 
```