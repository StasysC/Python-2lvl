# Darome Django vertimus

Viso Django puslapio kalbą galime pakeisti labai paprastai, tiesiog settings.py faile:

```python
LANGUAGE_CODE = 'lt'
```

Django automatiškai atvaizduoja visą administratoriaus puslapį lietuvių kalba. Tačiau taip neišverčiami mūsų sukurti laukai ir užrašai. Tai padarysime taip:

Iš pradžių į Windows įdiegiame reikiamas programas gettext ir iconv iš čia:
[https://mlocati.github.io/articles/gettext-iconv-windows.html](https://mlocati.github.io/articles/gettext-iconv-windows.html)

Padarykime vertimus puslapyje index.html:
```python
{% extends "base.html" %}
{% load i18n %}
{% block content %}
  <h1>{% trans "Local library" %}</h1>
  <p>{% trans "Welcome to my Library" %}</p>
  <p>{% trans "Today we have:" %}</p>
  <ul>
    <li><strong>{% trans "Books" %}:</strong> {{ num_books }}</li>
    <li><strong>{% trans "Book Instances" %}:</strong> {{ num_instances }}</li>
    <li><strong>{% trans "Now Available" %}:</strong> {{ num_instances_available }}</li>
    <li><strong>{% trans "Authors" %}:</strong> {{ num_authors }}</li>
  </ul>

<p>{% trans "Your visits:" %} {{ num_visits }}</p>
{% endblock %}
```

Pakeičiame modulių laukų, kintamųjų pavadinimus:
```python
from django.utils.translation import gettext as _

class Book(models.Model):
    title = models.CharField(_('Title'), max_length=200)
    author = models.ForeignKey('Author', on_delete=models.SET_NULL, null=True, related_name='books')
    summary = models.TextField(_('Summary'), max_length=1000, help_text='Trumpas knygos aprašymas')
    isbn = models.CharField('ISBN', max_length=13,
                            help_text='13 Simbolių <a href="https://www.isbn-international.org/content/what-isbn">ISBN kodas</a>')
    genre = models.ManyToManyField(Genre, help_text='Išrinkite žanrą(us) šiai knygai')
    cover = models.ImageField(_('Cover'), upload_to='covers', null=True)
```

Dabar mūsų programoje (library) sukuriame katalogą "locale" ir konsolėje paleidžiame šią komandą:
```console
django-admin makemessages -l lt
```
Django automatiškai sukurs vertimų failą .po, kurį galime atsidaryti su [POEdit](https://poedit.net/) programa, pasidaryti vertimus ir juos išsaugoti .mo faile (ten pat). Pabandykime perjungti kalbas ir pažiūrėti, ar pasikeičia kalbos išverstame puslapyje, taip pat išversto modelio admin puslapyje.

Jei norime, kad kalba būtų automatiškai parenkama pagal naršyklėje nustatytą kalbą, į settings.py pridedame 'django.middleware.locale.LocaleMiddleware':
```python
MIDDLEWARE = [
    'django.middleware.security.SecurityMiddleware',
    'django.contrib.sessions.middleware.SessionMiddleware',
    'django.middleware.common.CommonMiddleware',
    'django.middleware.locale.LocaleMiddleware',
    'django.middleware.csrf.CsrfViewMiddleware',
    'django.contrib.auth.middleware.AuthenticationMiddleware',
    'django.contrib.messages.middleware.MessageMiddleware',
    'django.middleware.clickjacking.XFrameOptionsMiddleware',
]
```