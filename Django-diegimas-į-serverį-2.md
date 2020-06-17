# Apsaugome jautrius Django duomenis

Linux serveryje susikuriame konfiguracinį json failą:
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
    "EMAIL_HOST_PASSWORD": "jusu_slaptazodis",                                          
}

```