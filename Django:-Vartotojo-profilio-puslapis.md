# Praplečiame vartotojo formą

Padarysime, kad prie vartotojo leistų prisegti nuotrauką. Ši informacija bus atvaizduojama naujame profilio puslapyje.

Sukuriame naują modelį faile models.py:
```python
class Profilis(models.Model):
    user = models.OneToOneField(User, on_delete=models.CASCADE)
    nuotrauka = models.ImageField(default="default.png", upload_to="profile_pics")

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
```html
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

Įdedame naują nuorodą į meniu, paveikslėlio ir vartotojo vardo tage, faile base.html:
```html
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

Kad vartotojui nepriskyrus jokios nuotraukos, būtų rodoma numatytoji, į media katalogą įdėkite failą default.png (numatytąjį paveikslėlį)

