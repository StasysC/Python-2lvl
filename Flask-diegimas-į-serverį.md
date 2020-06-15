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

```bash
vartotojas@ubuntu:~$ sudo apt install python3-pip
```
```bash
vartotojas@ubuntu:~$ sudo apt install python3-venv
```