# Create, Update, Delete rodinių klasės

## ListView klasė

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
        return BookInstance.objects.filter(reader=self.request.user).filter(status__exact='p').order_by('due_back')
```

Sukuriame path, faile library/urls:
```python
path('mybooks/', views.LoanedBooksByUserListView.as_view(), name='my-borrowed'),
```

Sukuriame html, faile user_books.html:
```python
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
        <a class="btn btn-primary" href="{{ bookinst.id }}" role="button">Peržiūrėti</a>
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

```