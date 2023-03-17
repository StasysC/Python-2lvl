# Praplečiame vartotojo formą
Padarysime, kad prie vartotojo leistų prisegti nuotrauką. Ši informacija bus atvaizduojama naujame profilio puslapyje.

Sukuriame naują modelį faile models.py:
```python
class Profilis(models.Model):
    user = models.OneToOneField(User, on_delete=models.CASCADE)
    nuotrauka = models.ImageField(default="profile_pics/default.png", upload_to="profile_pics")

    def __str__(self):
        return f"{self.user.username} profilis"
```
Sukuriame rodinį faile views.py:
```python
from django.contrib.auth.decorators import login_required

@login_required
def profilis(request):
    return render(request, 'profilis.html')
```
Įdedame naują urls'ą į library/urls:
```python
    path('profilis/', views.profilis, name='profilis'),
```
Galiausiai sukuriame naują profilis.html:
```python
{% extends "base.html" %}
{% block content %}
    <div class="content-section">
      <div class="media">
        <img class="rounded-circle account-img" src="{{ user.profilis.nuotrauka.url }}">
        <div class="media-body">
          <h2 class="account-heading">{{ user.username }}</h2>
          <p class="text-secondary">{{ user.email }}</p>
        </div>
      </div>
      <!-- FORM HERE -->
    </div>
{% endblock content %}
```
Įdedame į library/admin.py:
```python
from .models import Author, Genre, Book, BookInstance, BookReview, Profilis

admin.site.register(Profilis)
```
Įdedame naują nuorodą į meniu, paveikslėlio ir vartotojo vardo tage, faile base.html:
```python
        <ul class="navbar-nav ml-auto">
          {% if user.is_authenticated %}
            <li class="nav-item"><a class="nav-link" href="{% url 'profilis' %}">
              <svg class="bi bi-person" width="1.5em" height="1.5em" viewBox="0 0 16 16" fill="currentColor" xmlns="http://www.w3.org/2000/svg">
                <path fill-rule="evenodd" d="M13 14s1 0 1-1-1-4-6-4-6 3-6 4 1 1 1 1h10zm-9.995-.944v-.002.002zM3.022 13h9.956a.274.274 0 00.014-.002l.008-.002c-.001-.246-.154-.986-.832-1.664C11.516 10.68 10.289 10 8 10c-2.29 0-3.516.68-4.168 1.332-.678.678-.83 1.418-.832 1.664a1.05 1.05 0 00.022.004zm9.974.056v-.002.002zM8 7a2 2 0 100-4 2 2 0 000 4zm3-2a3 3 0 11-6 0 3 3 0 016 0z" clip-rule="evenodd"/>
              </svg>
            {{ user.get_username }}</a></li>
            <li class="nav-item"><a class="nav-link" href="{% url 'logout'%}?next=/library">Atsijungti</a></li>
          {% else %}
            <li class="nav-item"><a class="nav-link" href="{% url 'login'%}?next={{request.path}}">Prisijungti</a></li>
            <li class="nav-item"><a class="nav-link" href="{% url 'register'%}">Registruotis</a></li>
          {% endif %}
          {% if not user.is_authenticated %}
          {% endif %}
        </ul>
```
Nepamirštame migracijų!

Kad vartotojui nepriskyrus jokios nuotraukos, būtų rodoma numatytoji, į media katalogą įdėkite failą default.png (numatytąjį paveikslėlį)

# Susiejame vartotoją su profiliu
Šiame skyriuje padarysime, kad sukūrus vartotoją, būtų automatiškai sukurtas jo profilis.

**Dėmesio**: Prieš vartotojo ir profilio susiejimą, per admin puslapį rankiniu būdu kiekvienam vartotojui priskirkite profilį. Jeigu turite daug profilių, galima automatizuoti per django shell'ą (python manage.py shell) leidžiant nesudėtingą skriptą:
```python
>>> from django.contrib.auth.models import User
>>> from library.models import Profilis
>>>
>>> for u in User.objects.all():
...     try:
...         profile = Profilis(user=u)
...         profile.save()
...     except:
...         pass
```
Sukuriame failą library/signals.py:
```python
from django.db.models.signals import post_save  # signalas (būna įvairių)
from django.contrib.auth.models import User     # siuntėjas
from django.dispatch import receiver            # priėmėjas (dekoratorius)
from .models import Profilis

# Sukūrus vartotoją automatiškai sukuriamas ir profilis.
@receiver(post_save, sender=User) # jeigu išsaugojamas User objektas, inicijuojama f-ja po dekoratoriumi
def create_profile(sender, instance, created, **kwargs): # instance yra ką tik sukurtas User objektas.
    if created:
        Profilis.objects.create(user=instance)
        print('KWARGS: ', kwargs)


# Pakoregavus vartotoją, išsaugomas ir profilis
@receiver(post_save, sender=User)
def save_profile(sender, instance, **kwargs):
    instance.profilis.save()
```
Jei nėra, sukuriame failą library/apps.py:
```python
from django.apps import AppConfig


class LibraryConfig(AppConfig):
    name = 'library'

    def ready(self):
        from .signals import create_profile, save_profile
```
Įrašome į settings.py:
```python
INSTALLED_APPS = [
    'tinymce',
    'library.apps.LibraryConfig',
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
]
```
Susikuriame naują vartotoją per registracijos formą ir pasitikrinkite, ar automatiškai susikūrė jo profilis. Taip pat, ar profilio puslapyje matoma jo informacija (default nuotrauka).

# Padarome profilio puslapį redaguojamą
Šį kartą naudosime supaprastintas Crispy formas. Tam reikės įsidiegti tai:
```python
pip install django-crispy-forms
```
Įdėti į settings.py:
```python
INSTALLED_APPS = [
    'tinymce',
    'library.apps.LibraryConfig',
    'crispy_forms',
    'crispy_bootstrap4',
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
]
```
settings.py gale:
```python
CRISPY_TEMPLATE_PACK = 'bootstrap4'
```
Susikuriame vartotojo ir profilio atnaujinimo formas faile library/forms.py:
```python
from .models import Profilis
from django import forms
from django.contrib.auth.models import User

class BookReviewForm(forms.ModelForm):
    class Meta:
        model = BookReview
        fields = ('content', 'book', 'reviewer',)
        widgets = {'book': forms.HiddenInput(), 'reviewer': forms.HiddenInput()}

class UserUpdateForm(forms.ModelForm):
    email = forms.EmailField()

    class Meta:
        model = User
        fields = ['username', 'email']


class ProfilisUpdateForm(forms.ModelForm):
    class Meta:
        model = Profilis
        fields = ['nuotrauka']
```
Pakeičiame profilio rodinį taip, kad į puslapį būtų užkrautos abi anksčiau sukurtos formos, kartu su prieš tai buvusiais įrašais. Abi jas validavus, jos abi išsaugomos, pranešama apie sėkmingą atnaujinimą ir gražinama į tą patį puslapį. Faile views.py:
```python
from .forms import BookReviewForm, UserUpdateForm, ProfilisUpdateForm

@login_required
def profilis(request):
    if request.method == "POST":
        u_form = UserUpdateForm(request.POST, instance=request.user)
        p_form = ProfilisUpdateForm(request.POST, request.FILES, instance=request.user.profilis)
        if u_form.is_valid() and p_form.is_valid():
            u_form.save()
            p_form.save()
            messages.success(request, f"Profilis atnaujintas")
            return redirect('profilis')
    else:
        u_form = UserUpdateForm(instance=request.user)
        p_form = ProfilisUpdateForm(instance=request.user.profilis)

    context = {
        'u_form': u_form,
        'p_form': p_form,
    }
    return render(request, 'profilis.html', context)
```
Atnaujiname puslapį profilis.html:
```python
{% extends "base.html" %}
{% load crispy_forms_tags %}
{% block content %}
    <div class="content-section">
        {% if messages %}
        {% for message in messages %}
        <div class="alert alert-danger" role="alert">
            {{ message }}
        </div>
        {% endfor %}
        {% endif %}
      <div class="media">
        <img class="rounded-circle account-img" src="{{ user.profilis.nuotrauka.url }}">
        <div class="media-body">
          <h2 class="account-heading">{{ user.username }}</h2>
          <p class="text-secondary">{{ user.email }}</p>
        </div>
      </div>
       <form method="POST" enctype="multipart/form-data">
            {% csrf_token %}
            <fieldset class="form-group">
                <legend class="border-bottom mb-4">Profilio info</legend>
                {{ u_form|crispy }}
                {{ p_form|crispy }}
            </fieldset>
            <div class="form-group">
                <button class="btn btn-outline-info" type="submit">Atnaujinti</button>
            </div>
        </form>
    </div>
{% endblock content %}
```
# Automatiškai sumažiname ir atvaizduojame nuotraukas:
Profilio modelyje perrašome save metodą. Faile models.py:
```python
from PIL import Image

class Profilis(models.Model):
    user = models.OneToOneField(User, on_delete=models.CASCADE)
    nuotrauka = models.ImageField(default="default.png", upload_to="profile_pics")

    def __str__(self):
        return f"{self.user.username} profilis"

    def save(self, *args, **kwargs):
        super().save(*args, **kwargs)
        img = Image.open(self.nuotrauka.path)
        if img.height > 300 or img.width > 300:
            output_size = (300, 300)
            img.thumbnail(output_size)
            img.save(self.nuotrauka.path)
```
Dabar, prisegus naują failą profilyje, jis bus automatiškai sumažinamas iki 300x300 taškų.

Dabar galime vartotojo nuotraukas atvaizduoti ir puslapiuose, kurie turi ryšį su vartotoju, pavyzdžiui faile user_books.html:
```python
{% extends "base.html" %}

{% block content %}
    <h1>Mano paimtos knygos</h1>

    {% if bookinstance_list %}
    <ul>

      {% for bookinst in bookinstance_list %}
        <img class="rounded-circle" src="{{bookinst.reader.profilis.nuotrauka.url}}">
      <li class="{% if bookinst.is_overdue %}text-danger{% endif %}">
        <a href="{% url 'book-detail' bookinst.book.pk %}">{{bookinst.book.title}}</a> ({{ bookinst.due_back }})
      </li>
      {% endfor %}
    </ul>

    {% else %}
      <p>There are no books borrowed.</p>
    {% endif %}
{% endblock %}
```
## Užduotis
Tęsti kurti Django užduotį – [Autoservisas](https://github.com/StasysC/Python-2lvl/blob/master/Django/Autoservisas.md):
* Sukurti naują su vartotoju susietą profilio modelį su nuotraukos lauku, įdėti jį į admin ir išbandyti.
* Padaryti naują profilio puslapį, kuriame būtų atvaizduojamas profilio vardas, el. pašto adresas ir nuotrauka. Jei nuotrauka neprisegta, būtų rodoma default nuotrauka (ją reikia įdėti į media katalogą).
* Padaryti, kad sukūrus vartotoją, būtų automatiškai sukurtas ir jo profilis.
* Padaryti, kad profilio puslapyje būtų galima redaguoti vartotojo informaciją, pakeisti nuotrauką.
* Padaryti, kad prisegta profilio nuotrauka būtų automatiškai sumažinama iki norimo dydžio (pagal dizainą).
* Padaryti, kad vartotojo nuotrauka būtų matoma prie kiekvieno užsakymo.
