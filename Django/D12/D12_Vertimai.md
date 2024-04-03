# Darome Django vertimus
Viso Django puslapio kalbą galime pakeisti labai paprastai, tiesiog settings.py faile:
```python
LANGUAGE_CODE = 'lt'
```
Django automatiškai atvaizduoja visą administratoriaus puslapį lietuvių kalba. Tačiau taip neišverčiami mūsų sukurti laukai ir užrašai. Tai padarysime taip:

## Darome vertimus mūsų puslapiuose
Iš pradžių į Windows įdiegiame reikiamas programas gettext ir iconv iš čia: https://mlocati.github.io/articles/gettext-iconv-windows.html

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
Pakeičiame modulių laukų pavadinimus:
```python
from django.utils.translation import gettext_lazy as _

class Book(models.Model):
    """Modelis reprezentuoja knygą (bet ne specifinę knygos kopiją)"""
    title = models.CharField(_('Title'), max_length=200)
    author = models.ForeignKey('Author', on_delete=models.SET_NULL, null=True, related_name='books')
    summary = models.TextField(_('Summary'), max_length=1000, help_text=_('Shot book summary'))
    isbn = models.CharField('ISBN', max_length=13,
                            help_text='13 Simbolių <a href="https://www.isbn-international.org/content/what-isbn">ISBN kodas</a>')
    genre = models.ManyToManyField(Genre, help_text=_('Please choose genres'))
    # genre = models.ForeignKey('Žanras', Genre)
    cover = models.ImageField(_('Cover'), upload_to='covers', null=True)
```
Išverčiame pranešimų žinutes:
```python
from django.utils.translation import gettext as _

@csrf_protect
def register(request):
    if request.method == "POST":
        # pasiimame reikšmes iš registracijos formos
        username = request.POST['username']
        email = request.POST['email']
        password = request.POST['password']
        password2 = request.POST['password2']
        # tikriname, ar sutampa slaptažodžiai
        if password == password2:
            # tikriname, ar neužimtas username
            if User.objects.filter(username=username).exists():
                messages.error(request, _('Username %s already exists!') % username)
                return redirect('register')
            else:
                # tikriname, ar nėra tokio pat email
                if User.objects.filter(email=email).exists():
                    messages.error(request, _('Email %s already exists!') % email)
                    return redirect('register')
                else:
                    # jeigu viskas tvarkoje, sukuriame naują vartotoją
                    User.objects.create_user(username=username, email=email, password=password)
        else:
            messages.error(request, _('Passwords do not match!'))
            return redirect('register')
    return render(request, 'register.html')
```
Tuose failuose, kuriuos django leidžia vieną kartą (models.py, forms.py) reikėtų importuoti gettext_lazy, tuose, kuriuos naudoja nuolat, pvz views.py, importuojame gettext. Dabar mūsų projekte sukuriame katalogą "locale" ir konsolėje paleidžiame šią komandą:
```python
django-admin makemessages -l lt
```
Django automatiškai sukurs vertimų failą .po, kurį galime atsidaryti su POEdit programa, pasidaryti vertimus ir juos išsaugoti .mo faile (ten pat). Pabandykime perjungti kalbas ir pažiūrėti, ar pasikeičia kalbos išverstame puslapyje, taip pat išversto modelio admin puslapyje.

Sukompiliuojame vertimus, kad Django galėtų juos naudoti:
```python
python manage.py compilemessages
```
Taip pat galima išversti visą html kodo bloką, įdėjus {% blocktrans %} ir {% endblocktrans %}, pvz.:
```python
<h1>
  <a href="/" title="{% blocktrans %}Back to '{{ race }}' homepage{% endblocktrans %}">{{ race }}</a>
</h1>
```
## Modifikuojame setting.py file
Į settings.py pridedame 'django.middleware.locale.LocaleMiddleware':
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
nustatome, kur ieškos locale aplanko:

```python
LOCALE_PATHS = (os.path.join(BASE_DIR, 'locale'),)
```
## Dedame kalbos pasirinkimo formą
Galime į puslapį įdėti kalbos pasirinkimo formą. Tam:

Į settings.py dedame:
```python
from django.utils.translation import gettext_lazy as _

LANGUAGES = (
    ('en-us', _('English')),
    ('lt', _('Lithuanian')),
)
```
Į library/urls.py pridedame:
```python
    path('i18n/', include('django.conf.urls.i18n')),
```
Ten, kur norime turėti kalbos pasirinkimo formą, dedame šį kodą (pvz. į base.html meniu):
```python
        {% load i18n %}
      <form action="{% url 'set_language' %}" method="post">
        {% csrf_token %}
        <input name="next" type="hidden" value="{{ redirect_to }}"/>
        <select name="language" onchange="this.form.submit()">
          {% load static %}
          {% get_current_language as LANGUAGE_CODE %}
          {% get_available_languages as LANGUAGES %}
          {% for lang in LANGUAGES %}
          <option style="background-image: url({% static 'img/lt.png' %});" value="{{ lang.0 }}" {% if lang.0 == LANGUAGE_CODE %} selected="selected" {% endif %}>
            {{ lang.1 }}
          </option>
          {% endfor %}
        </select>
      </form>
```

## Užduotis
Tęsti kurti Django užduotį – [Autoservisas](https://github.com/StasysC/Python-2lvl/blob/master/Django/Autoservisas.md):

* Visus užrašus, kintamuosius (kiek įmanoma) aprašyti anglų kalba.
* Padaryti vertimus, kad perjungus iš anglų kalbos į lietuvių, automatiškai išsiverstų visi užrašai.
* Padaryti mygtukus (arba pasirinkimą), kuris leistų pasirinkti puslapio kalbą.
