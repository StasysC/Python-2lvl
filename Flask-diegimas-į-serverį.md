# Flask diegimas į serverį

Savo projekte sukuriame requirements.txt failą (žr. temą virtualios aplinkos)

Per FTP programą įsirašome savo flask programos katalogą į /home/vartotojas/.

Pvz.:
Iš Desktop katalogą biudzetas per WINSCP nukopijuojame į /home/vartotojas/

Jei reikia, serveryje įdiegiame openssh:
```bash
vartotojas@ubuntu:~$ sudo apt install openssh-server
```

Prisijungiame prie mūsų serverio su cmd (jei sukurtas vartotojas - per jį, jei ne - per root):
```cmd
C:\Users\Donoras>ssh vartotojas@192.168.43.108
```

Serveryje atnaujiname programas:
```bash
vartotojas@ubuntu:~$ sudo apt update && apt upgrade  
```

### Susikuriame virtualią aplinką:

Įdiegiame pip:
```bash
vartotojas@ubuntu:~$ sudo apt install python3-pip
```
Įdiegiame venv:
```bash
vartotojas@ubuntu:~$ sudo apt install python3-venv
```
Sukuriame venv:
```bash
vartotojas@ubuntu:~$ python3 -m venv biudzetas/venv
```
Aktyvuojame sukurtą aplinką:
```bash
vartotojas@ubuntu:~$ cd biudzetas/
vartotojas@ubuntu:~/biudzetas$ source venv/bin/activate
```
Įdiegiame programas iš requirements.txt failo:
```bash
(venv) vartotojas@ubuntu:~/biudzetas$ pip install -r requirements.txt
```

### Nustatome app kintamąjį ir išbandome programą:

```bash
(venv) vartotojas@ubuntu:~/biudzetas$ export FLASK_APP=run.py
(venv) vartotojas@ubuntu:~/biudzetas$ flask run --host=0.0.0.0
```

Galime kompiuterio naršyklėje užeiti į IP ir portą ir patikrinti, ar veikia programa, pvz.:
http://192.168.43.108:5000/

Matome užrašą:
WARNING: This is a development server. Do not use it in a production deployment.
Todėl toks paleidimas tinka tik kūrimo tikslams. Normaliam veikimui serveryje mums reikės programų nginx ir gunicorn.

Sustabdome procesą cmd programoje paspaudę CTRL+C

### Diegiame ngnix ir gunicorn:
```bash
(venv) vartotojas@ubuntu:~/biudzetas$ cd
(venv) vartotojas@ubuntu:~$ sudo apt install nginx
(venv) vartotojas@ubuntu:~$ pip install gunicorn
```

### Konfiguruojame ngnix:
```bash
(venv) vartotojas@ubuntu:~$ sudo rm /etc/nginx/sites-enabled/default
(venv) vartotojas@ubuntu:~$ sudo nano /etc/nginx/sites-enabled/biudzetas
```

Šiame faile įdedame tokį kodą:

Prie server_name įrašome savo serverio IP

Į location /static - kelia iki programos static katalogo

```
server {
    listen 80;
    server_name 192.168.43.108;

    location /static {
        alias /home/vartotojas/biudzetas/biudzetas/static;
    }

    location / {
        proxy_pass http://localhost:8000;
        include /etc/nginx/proxy_params;
        proxy_redirect off;
    }
}

```

Perkrauname nginx:
```bash
(venv) vartotojas@ubuntu:~$ sudo systemctl restart nginx
```

Jei naršyklėje atidarysime http://192.168.43.108/, pamatysime, kad programa vis dar neveikia (nginx klaida)

### Konfiguruojame ir paleidžiame gunicorn:
Sužinome, kiek mūsų serveris turi branduolių:
```bash
(venv) vartotojas@ubuntu:~$ nproc --all
1
```
Reiškia, paleisdami gunicorn, prie -w turėsime įrašyti 3 ((2 x branduolių_kiekis) + 1)

Paleidžiame gunicorn:
```bash
(venv) vartotojas@ubuntu:~$ cd biudzetas/
(venv) vartotojas@ubuntu:~/biudzetas$ gunicorn -w 3 run:app
```

Galime užeiti į naršyklę ir pažiūrėti, ar viskas veikia, pvz.: http://192.168.43.108/