
# Django Technical Cheat Sheet

##  Project Structure

```bash
django-admin startproject myproject
cd myproject
python manage.py startapp myapp
```

### Django Project Files:
```
myproject/
├── manage.py
├── myproject/
│   ├── settings.py
│   ├── urls.py
│   ├── wsgi.py
│   └── asgi.py
├── myapp/
│   ├── models.py
│   ├── views.py
│   ├── urls.py (create this manually)
│   ├── templates/
│   └── static/
```

##  Settings Highlights (`settings.py`)

```python
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    ...
    'myapp',  # your app
]

DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',  # or postgresql
        'NAME': BASE_DIR / "db.sqlite3",
    }
}

TEMPLATES = [
    {
        'DIRS': [BASE_DIR / 'templates'],
        ...
    }
]

STATIC_URL = '/static/'
MEDIA_URL = '/media/'
```

## Models (`models.py`)

```python
from django.db import models

class Post(models.Model):
    title = models.CharField(max_length=100)
    content = models.TextField()
    published = models.DateTimeField(auto_now_add=True)

    def __str__(self):
        return self.title
```

```bash
python manage.py makemigrations
python manage.py migrate
```

##  ORM Queries

```python
Post.objects.all()
Post.objects.filter(title__icontains="django")
Post.objects.get(id=1)
Post.objects.create(title="Django", content="Framework")
Post.objects.update_or_create(...)
```

##  Admin Setup

```python
from django.contrib import admin
from .models import Post

admin.site.register(Post)
```

Create superuser:
```bash
python manage.py createsuperuser
```

##  URLs

### Project-level `urls.py`:

```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('myapp.urls')),
]
```

### App-level `urls.py` (create it):

```python
from django.urls import path
from . import views

urlpatterns = [
    path('', views.index, name='index'),
]
```

##  Views

```python
from django.shortcuts import render
from .models import Post

def index(request):
    posts = Post.objects.all()
    return render(request, 'index.html', {'posts': posts})
```

##  Templates

```html
<!-- templates/index.html -->
{% extends "base.html" %}

{% block content %}
  <h1>Posts</h1>
  {% for post in posts %}
    <h3>{{ post.title }}</h3>
    <p>{{ post.content }}</p>
  {% endfor %}
{% endblock %}
```

##  Static & Media Files

### settings.py:
```python
STATICFILES_DIRS = [BASE_DIR / "static"]
MEDIA_ROOT = BASE_DIR / "media"
MEDIA_URL = "/media/"
```

### urls.py:
```python
from django.conf import settings
from django.conf.urls.static import static

urlpatterns += static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)
```

##  Forms

```python
from django import forms
from .models import Post

class PostForm(forms.ModelForm):
    class Meta:
        model = Post
        fields = ['title', 'content']
```

```python
def create_post(request):
    if request.method == 'POST':
        form = PostForm(request.POST)
        if form.is_valid():
            form.save()
    else:
        form = PostForm()
    return render(request, 'create.html', {'form': form})
```

##  Useful Commands

| Command                            | Description                         |
|-----------------------------------|-------------------------------------|
| `python manage.py runserver`      | Start dev server                    |
| `python manage.py makemigrations` | Prepare DB changes                  |
| `python manage.py migrate`        | Apply DB changes                    |
| `python manage.py shell`          | Start Django shell                  |
| `python manage.py createsuperuser`| Create admin user                   |
| `python manage.py startapp <name>`| Start a new app                     |

##  Debug Tips

- Add `'django_extensions'` for shell_plus, graph_models
- Use `print()` or `pdb.set_trace()` for debugging
- Use `django-debug-toolbar` in dev

##  Best Practices

- Use `.env` for secrets and DB config (e.g., `django-environ`)
- Split settings into `base.py`, `dev.py`, `prod.py`
- Use Class-Based Views (`ListView`, `DetailView`) for large apps
- Structure templates with includes and blocks


---

##  Class-Based Views (CBVs)

### ListView Example
```python
from django.views.generic import ListView
from .models import Post

class PostListView(ListView):
    model = Post
    template_name = 'posts.html'
    context_object_name = 'posts'
```

### DetailView Example
```python
from django.views.generic import DetailView

class PostDetailView(DetailView):
    model = Post
    template_name = 'post_detail.html'
```

---

##  Middleware

### Example middleware
```python
# myapp/middleware.py
class SimpleMiddleware:
    def __init__(self, get_response):
        self.get_response = get_response

    def __call__(self, request):
        print("Before view")
        response = self.get_response(request)
        print("After view")
        return response
```

### Register it:
```python
MIDDLEWARE = [
    ...
    'myapp.middleware.SimpleMiddleware',
]
```

---

##  Template Tags & Filters

### Common Template Tags
```django
{% if condition %}
{% for item in list %}
{% include 'file.html' %}
{% block content %}{% endblock %}
```

### Filters
```django
{{ value|length }}
{{ date|date:"Y-m-d" }}
{{ name|upper }}
```

---

##  Authentication
### Login/Logout URLs
```python
from django.contrib.auth import views as auth_views

urlpatterns = [
    path('login/', auth_views.LoginView.as_view(), name='login'),
    path('logout/', auth_views.LogoutView.as_view(), name='logout'),
]
```

### Login Required Decorator
```python
from django.contrib.auth.decorators import login_required

@login_required
def dashboard(request):
    ...
```

---

##  File Uploads

### Model
```python
class Upload(models.Model):
    title = models.CharField(max_length=100)
    file = models.FileField(upload_to='uploads/')
```

### Form
```python
class UploadForm(forms.ModelForm):
    class Meta:
        model = Upload
        fields = ['title', 'file']
```

### View
```python
def upload_file(request):
    if request.method == 'POST':
        form = UploadForm(request.POST, request.FILES)
        if form.is_valid():
            form.save()
    else:
        form = UploadForm()
    return render(request, 'upload.html', {'form': form})
```

---

## Internationalization (i18n)

### Enable in settings.py
```python
LANGUAGE_CODE = 'en-us'
USE_I18N = True
```

### Template Usage
```django
{% load i18n %}
{% trans "Hello" %}
```

---

##  Custom Management Commands

```python
# myapp/management/commands/hello.py
from django.core.management.base import BaseCommand

class Command(BaseCommand):
    def handle(self, *args, **kwargs):
        self.stdout.write("Hello from custom command")
```

Run:
```bash
python manage.py hello
```

---
