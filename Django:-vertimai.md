# Keičiame bendrą Django puslapio kalbą

Viso Django puslapio kalbą galime pakeisti labai paprastai, tiesiog settings.py faile:

```python
LANGUAGE_CODE = 'lt'
```

Django automatiškai atvaizduoja visą administratoriaus puslapį lietuvių kalba. Tačiau taip neišverčiami mūsų sukurti laukai ir užrašai. Tai padarysime taip:

Iš pradžių į Windows įdiegiame reikiamas programas gettext ir iconv iš čia:
[https://mlocati.github.io/articles/gettext-iconv-windows.html](https://mlocati.github.io/articles/gettext-iconv-windows.html)

# Išverčiame užrašus puslapyje:

Padarykite vertimus puslapyje index.html:



# Modulių laukų, kintamųjų pavadinimai: