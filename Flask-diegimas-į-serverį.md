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

Galime kompiuterio naršyklėje užeiti į IP ir portą ir patikrinti, ar veikia programa:
http://192.168.43.108:5000/

Sustabdome procesą cmd programoje paspaudę CTRL+C

