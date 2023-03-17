# Create, Update, Delete rodinių klasės
## ListView klasė
**Dėmesio**: perdaryti bookinstance klasę, kad pk būtų standartinis. Arba naudoti urlpatternuose str:pk arba uuid:pk, o viewsuose user_books.html href attributuose nurodyti bookinst.pk :)

Iš pradžių sukuriame (patobuliname jau įprastą ListView). Tam, kad šį puslapį galėtų peržiūrėti tik prisijungę vartotojai, paveldime LoginRequiredMixin. Faile library/views:
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
Sukuriame html. Jei objekto pavadinimas nenurodytas, jo laukus pasiekiame per object.. Faile user_book.html:
```python
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
## CreateView klasė
```python
from django.views.generic import (
    ListView,
    DetailView,
    CreateView,
)

class BookByUserCreateView(LoginRequiredMixin, CreateView):
    model = BookInstance
    fields = ['book', 'due_back']
    success_url = "/library/mybooks/"
    template_name = 'user_book_form.html'

    def form_valid(self, form):
        form.instance.reader = self.request.user
        return super().form_valid(form)
```
Sukuriame path, faile library/urls:
```python
path('mybooks/new', views.BookByUserCreateView.as_view(), name='my-borrowed-new'),
```
Prie knygos egzemplioriaus pridedame metodą:
```python
    def get_absolute_url(self):
        """Nurodo konkretaus aprašymo galinį adresą"""
        return reverse('book-detail', args=[str(self.id)])
```
Sukuriame html, faile user_book_form.html:
```python
{% extends "base.html" %}
{% load crispy_forms_tags %}
{% block content %}
    <div class="content-section">
    <form method="POST">
        {% csrf_token %}
        <fieldset class="form-group">
            <legend class="border-bottom mb-4">Naujas knygos egzempliorius</legend>
            {{ form|crispy }}
        </fieldset>
        <div class="form-group">
            <button class="btn btn-outline-info" type="submit">Išsaugoti</button>
        </div>
    </form>
    </div>
{% endblock content %}
```
Įdedame į savo meniu naują punktą, faile base.html:
```python
<li class="nav-item"><a class="nav-link" href="{% url 'my-borrowed-new'%}?next=/library">{% trans "New" %}</a></li>
```
PAPILDOMAI:

Jei CreateView view'e prireiktų į formą įdėti kintamąjį (id lauką) iš URL adreso, galime padaryti pavyzdžiui taip:
```python
def form_valid(self, form):
    form.instance.reader = User.objects.get(pk=self.kwargs['pk'])
    return super().form_valid(form)    
```
## UpdateView klasė
Kad knygos įrašą leistų atnaujinti tik tam vartotojui, kuris yra nurodytas jos reader lauke, paveldime UserPassesTestMixin ir perrašome metodą test_func, kuris gražina True tik tuomet, kai reader laukas sutampa su prisijungusiu vartotoju.
```python
from django.contrib.auth.mixins import UserPassesTestMixin

from django.views.generic import (
    ListView,
    DetailView,
    CreateView,
    UpdateView,
)

class BookByUserUpdateView(LoginRequiredMixin, UserPassesTestMixin, UpdateView):
    model = BookInstance
    fields = ['book', 'due_back']
    success_url = "/library/mybooks/"
    template_name = 'user_book_form.html'

    def form_valid(self, form):
        form.instance.reader = self.request.user
        return super().form_valid(form)

    def test_func(self):
        book = self.get_object()
        return self.request.user == book.reader
```
Sukuriame path, faile library/urls:
```python
    path('mybooks/<int:pk>/update', views.BookByUserUpdateView.as_view(), name='my-book-update'),
```
Įdedame atnaujinimo nuorodą į failą user_book.html:
```python
        <li><strong>Gražinimo terminas:</strong> {{object.due_back}}</li>
            {% if object.reader == user %}
            <div>
                <a class="btn btn-secondary btn-sm mt-1 mb-1" href="{% url 'my-book-update' object.id %}">Redaguoti</a>
            </div>
            {% endif %}
```
## DeleteView klasė
```python
from django.views.generic import (
    ListView,
    DetailView,
    CreateView,
    UpdateView,
    DeleteView,
)

class BookByUserDeleteView(LoginRequiredMixin, UserPassesTestMixin, DeleteView):
    model = BookInstance
    success_url = "/library/mybooks/"
    template_name = 'user_book_delete.html'

    def test_func(self):
        book = self.get_object()
        return self.request.user == book.reader
```
Sukuriame path, faile library/urls:
```python
path('mybooks/<int:pk>/delete', views.BookByUserDeleteView.as_view(), name='my-book-delete'),
```
Sukuriame html, faile user_book_delete.html:
```python
{% extends "base.html" %}
{% load crispy_forms_tags %}
{% block content %}
    <div class="content-section">
    <form method="POST">
        {% csrf_token %}
        <fieldset class="form-group">
            <legend class="border-bottom mb-4">Ištrinti knygą</legend>
            <h2>Ar tikrai norite ištrinti knygą {{ object.uuid }}?</h2>
        </fieldset>
        <div class="form-group">
            <button class="btn btn-outline-danger" type="submit">Taip, ištrinti</button>
            <a class="btn btn-outline-secondary" href="{% url 'my-book' object.id %}">Atšaukti</a>
        </div>
    </form>
    </div>
{% endblock content %}
```
Įdedame trynimo nuorodą į failą user_book.html:
```python
        <li><strong>Gražinimo terminas:</strong> {{object.due_back}}</li>
            {% if object.reader == user %}
            <div>
                <a class="btn btn-secondary btn-sm mt-1 mb-1" href="{% url 'my-book-update' object.id %}">Redaguoti</a>
                <a class="btn btn-danger btn-sm mt-1 mb-1" href="{% url 'my-book-delete' object.id %}">Ištrinti</a>
            </div>
            {% endif %}
```
## Kaip padaryti patogesnį datos/laiko įvedimą (datepicker)
models.py faile, modelyje turi būti DateField (arba DateTimeField?):
```python
class BookInstance(models.Model):
    """Modelis, aprašantis konkrečios knygos kopijos būseną"""
    book = models.ForeignKey('Book', on_delete=models.SET_NULL, null=True)
    due_back = models.DateField('Bus prieinama', null=True, blank=True)
    reader = models.ForeignKey(User, on_delete=models.SET_NULL, null=True, blank=True)
```
view.py faile, CreateView klasėje:
```python
class BookByUserCreateView(LoginRequiredMixin, CreateView):
    model = BookInstance
    # fields = ['book', 'due_back']
    success_url = "/library/mybooks/"
    template_name = 'user_book_form.html'
    form_class = UserBookCreateForm

    def form_valid(self, form):
        form.instance.reader = self.request.user
        return super().form_valid(form)
```
forms.py faile, nauja forma ir papildoma klasė:
```python
from .models import BookReview, Profilis, BookInstance

class DateInput(forms.DateInput):
    input_type = 'date'

class UserBookCreateForm(forms.ModelForm):
    class Meta:
        model = BookInstance
        fields = ['book', 'reader', 'due_back']
        widgets = {'reader': forms.HiddenInput(), 'due_back': DateInput()}
```
user_book_form.html faile:
```python
{% extends "base.html" %}
{% load crispy_forms_tags %}
{% block content %}
    <div class="content-section">
    <form method="POST" action="" enctype="multipart/form-data">
        {% csrf_token %}
        <fieldset class="form-group">
            <legend class="border-bottom mb-4">Naujas knygos egzempliorius</legend>
            {{ form|crispy }}
        </fieldset>
        <div class="form-group">
            <button class="btn btn-outline-info" type="submit">Išsaugoti</button>
        </div>
    </form>
    </div>
{% endblock content %}
```
[Šio patarimo nuoroda](https://webpedia.net/how-to-use-datepicker-in-django)

## Užduotis
Tęsti kurti Django užduotį – [Autoservisas](https://github.com/StasysC/Python-2lvl/blob/master/Django/Autoservisas.md):

* Jei reikia, perdaryti vartotojo užsakymų puslapius į ListView ir DetailView klases.
* Padaryti, kad prisijungęs vartotojas galėtų kurti naujus užsakymus (be eilučių, tik pasirinkęs automobilį ir terminą). Panaudoti CreateView
* Padaryti, kad prisijungęs vartotojas galėtų redaguoti savo užsakymus. Panaudoti UpdateView
* Padaryti, kad prisijungęs vartotojas galėtų ištrinti savo užsakymus. Panaudoti DeleteView
* Padaryti, kuriant užsakymą, datą ir laiką leistų pasirinkti kalendoriuje/laikrodyje (datetimepicker)
## Papildoma užduotis
* Padaryti, kad vartotojas galėtų savo užsakyme įvesti eilutes (pasirinktas paslaugas ir kiekius). Papildomai - padaryti, kad šias eilutes galima būtų redaguoti/ištrinti.
