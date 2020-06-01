# Praplečiame vartotojo formą

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
```