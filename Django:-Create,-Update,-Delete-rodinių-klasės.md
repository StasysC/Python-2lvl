# Create, Update, Delete rodinių klasės

## ListView klasė

**Dėmesio:** perdaryti bookinstance klasę, kad pk būtų standartinis.

Iš pradžių sukuriame (patobuliname jau įprastą ListView), faile library/views:
```python
from django.contrib.auth.mixins import LoginRequiredMixin
from django.views.generic import ListView

class LoanedBooksByUserListView(LoginRequiredMixin, ListView):
    model = BookInstance
    context_object_name = 'books'
    template_name = 'user_books.html'
    paginate_by = 10

    def get_queryset(self):
        return BookInstance.objects.filter(reader=self.request.user).order_by('due_back')
```

Sukuriame path, faile library/urls:
```python
path('mybooks/', views.LoanedBooksByUserListView.as_view(), name='my-borrowed'),
```

Sukuriame html, faile user_books.html:
```html
{% extends "base.html" %}

{% block content %}
    <h1>Mano paimtos knygos</h1>
    {% if books %}
        {% for bookinst in books %}
    <hr>
        <ul>

        <img class="rounded-circle" src="{{bookinst.reader.profilis.nuotrauka.url}}">
        <li><strong class="{% if bookinst.is_overdue %}text-danger{% endif %}">Pavadinimas: {{bookinst.book.title}}</strong></li>
        <li><strong>Gražinimo terminas:</strong> {{bookinst.due_back}}</li>
        <br/>
        <a class="btn btn-primary" href="{{ bookinst.pk }}" role="button">Peržiūrėti</a>
      </li>

    </ul>
{% endfor %}
    {% else %}
      <p>There are no books borrowed.</p>
    {% endif %}
{% endblock %}
```

## DetailView klasė
```python
from django.views.generic import (
    ListView,
    DetailView,
)

class BookByUserDetailView(LoginRequiredMixin, DetailView):
    model = BookInstance
    template_name = 'user_book.html'
```

Sukuriame path, faile library/urls:
```python
path('mybooks/<int:pk>', views.BookByUserDetailView.as_view(), name='my-book'),
```

Sukuriame html, faile user_book.html:
```html
{% extends "base.html" %}

{% block content %}
    <h1>Mano paimta knyga:</h1>
    <hr>
        <ul>
        <img class="rounded-circle" src="{{object.reader.profilis.nuotrauka.url}}">
        <li><strong class="{% if object.is_overdue %}text-danger{% endif %}">Pavadinimas: {{object.book.title}}</strong></li>
        <li><strong>Gražinimo terminas:</strong> {{object.due_back}}</li>
        <br/>
      </li>
    </ul>
{% endblock %}
```