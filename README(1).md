# ☕ Jinja2 & Django Apps

> A beginner-friendly Django learning project focused on **Django apps, URL routing, views, templates, template inheritance, and Jinja2-style syntax**.

![Python](https://img.shields.io/badge/Python-3.x-blue?logo=python&logoColor=white)
![Django](https://img.shields.io/badge/Django-Web%20Framework-092E20?logo=django&logoColor=white)
![HTML](https://img.shields.io/badge/HTML-Templates-E34F26?logo=html5&logoColor=white)
![VS Code](https://img.shields.io/badge/Editor-VS%20Code-007ACC?logo=visualstudiocode&logoColor=white)

---

## 📌 Project Overview

This project is created to understand the basic structure of a **Django application** and how different components communicate with each other.

### Concepts Covered

- Creating a Django app
- Registering an app in `INSTALLED_APPS`
- Creating and connecting `urls.py`
- Creating Django views
- Using `include()` for app-level URL routing
- Working with Django HTML templates
- Understanding Jinja2-style template syntax
- Configuring Emmet for Django HTML in VS Code
- Understanding the Django request/response flow

### 🔄 Core Flow

```text
Browser
   ↓
URL
   ↓
urls.py
   ↓
View
   ↓
Template / Response
   ↓
Browser
```

---

## 🛠️ Technologies Used

| Technology | Purpose |
|---|---|
| **Python** | Programming language |
| **Django** | Web framework |
| **Django Template Language (DTL)** | Default Django template system |
| **Jinja2 concepts** | Template syntax and comparison |
| **HTML** | Web page structure |
| **VS Code** | Development environment |

---

# 🚀 Getting Started

## Prerequisites

Make sure Python and Django are installed on your system.

You can verify Python with:

```bash
python --version
```

---

## 1. Create a Django Project

Create a new Django project:

```bash
django-admin startproject myproject
```

Move into the project directory:

```bash
cd myproject
```

Start the development server:

```bash
py manage.py runserver
```

The application will normally be available at:

```text
http://127.0.0.1:8000/
```

---

# 📦 Creating a Django App

Create an app named `chai`:

```bash
py manage.py startapp chai
```

This creates a structure similar to:

```text
chai/
├── __init__.py
├── admin.py
├── apps.py
├── migrations/
│   └── __init__.py
├── models.py
├── tests.py
└── views.py
```

### Project vs App

A **Django project** represents the complete website/application, while a **Django app** represents a specific feature or module.

For example:

```text
Project
│
├── chai       → Chai-related functionality
├── accounts   → Authentication
├── products   → Products
└── blog       → Blog
```

---

# ⚙️ Register the App

Open:

```text
myproject/settings.py
```

Add `chai` to `INSTALLED_APPS`:

```python
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',

    'chai',
]
```

This tells Django that the `chai` application is part of the project.

---

# 🔗 URL Routing

Django uses URL configurations to decide which view should handle a request.

There are generally two levels of URL configuration:

```text
Project URLs
     ↓
App URLs
     ↓
View
```

## Main `urls.py`

The project's main `urls.py` can contain:

```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('chai/', include('chai.urls')),
]
```

The important part is:

```python
path('chai/', include('chai.urls')),
```

This tells Django:

> Any URL beginning with `/chai/` should be handled by `chai/urls.py`.

---

# 🧭 App-Level `urls.py`

Django does not automatically create `urls.py` when creating an app.

Create it manually:

```text
chai/
├── views.py
├── models.py
├── admin.py
├── apps.py
└── urls.py
```

Add:

```python
from django.urls import path
from . import views

urlpatterns = [
    path('', views.home, name='home'),
    path('about/', views.about, name='about'),
    path('contact/', views.contact, name='contact'),
]
```

---

# 👀 Views

Open:

```text
chai/views.py
```

Example:

```python
from django.http import HttpResponse


def home(request):
    return HttpResponse("Welcome to Chai!")


def about(request):
    return HttpResponse("About Chai")


def contact(request):
    return HttpResponse("Contact Chai")
```

A view receives an HTTP request and returns an HTTP response.

For example:

```python
def home(request):
    return HttpResponse("Welcome to Chai!")
```

The flow is:

```text
/chai/
   ↓
views.home()
   ↓
"Welcome to Chai!"
```

---

# 🔍 Understanding `include()`

Suppose the main project has:

```python
path('chai/', include('chai.urls')),
```

And `chai/urls.py` contains:

```python
path('menu/', views.menu, name='menu'),
```

Django combines them:

```text
/chai/ + menu/
```

Result:

```text
/chai/menu/
```

### Complete Routing Flow

```text
Browser
   │
   │  /chai/menu/
   ↓
project/urls.py
   │
   │  include('chai.urls')
   ↓
chai/urls.py
   │
   │  path('menu/', views.menu)
   ↓
views.menu()
   ↓
Response
```

---

# 🏷️ Named URLs

URLs can be given names:

```python
path('about/', views.about, name='about'),
```

The name:

```text
about
```

can be used inside templates:

```html
<a href="{% url 'about' %}">About</a>
```

This is better than hard-coding:

```html
<a href="/chai/about/">About</a>
```

Named URLs make applications easier to maintain.

---

# 🎨 Django Templates

Instead of returning plain text:

```python
return HttpResponse("Welcome to Chai!")
```

we can render an HTML template.

Use:

```python
from django.shortcuts import render


def home(request):
    return render(request, 'chai/home.html')
```

### Recommended Template Structure

```text
chai/
└── templates/
    └── chai/
        ├── home.html
        ├── about.html
        └── contact.html
```

Example `home.html`:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Chai Home</title>
</head>

<body>

    <h1>Welcome to Chai!</h1>

</body>
</html>
```

---

# 🧩 Template Syntax

Django templates use special syntax.

## Variables

```html
<h1>{{ name }}</h1>
```

If the view sends:

```python
return render(
    request,
    'chai/home.html',
    {'name': 'Masala Chai'}
)
```

the template can display:

```text
Masala Chai
```

---

## Conditions

```html
{% if user %}
    <p>Welcome!</p>
{% else %}
    <p>Please log in.</p>
{% endif %}
```

---

## Loops

```html
{% for chai in chais %}
    <p>{{ chai }}</p>
{% endfor %}
```

---

## URL Tags

```html
<a href="{% url 'home' %}">Home</a>
```

---

## Comments

Single-line template comments:

```html
{# This is a template comment #}
```

Multi-line comments:

```html
{% comment %}
This is a multi-line comment.
{% endcomment %}
```

---

# 🧱 Template Inheritance

One of the most useful Django template features is **template inheritance**.

Create:

```text
templates/
└── base.html
```

Example:

```html
<!DOCTYPE html>
<html>

<head>
    <title>{% block title %}Chai App{% endblock %}</title>
</head>

<body>

    <nav>
        <a href="{% url 'home' %}">Home</a>
        <a href="{% url 'about' %}">About</a>
        <a href="{% url 'contact' %}">Contact</a>
    </nav>

    {% block content %}
    {% endblock %}

</body>

</html>
```

Then another template can extend it:

```html
{% extends "base.html" %}

{% block title %}
Home
{% endblock %}

{% block content %}

<h1>Welcome to Chai!</h1>

{% endblock %}
```

### Why Use Template Inheritance?

It avoids repeating the same HTML structure on every page and makes templates easier to maintain.

---

# 🟢 Jinja2 vs Django Templates

Jinja2 and Django Template Language have very similar syntax.

### Variable

```html
{{ name }}
```

### Condition

```html
{% if user %}
    Hello {{ user }}
{% endif %}
```

### Loop

```html
{% for item in items %}
    {{ item }}
{% endfor %}
```

However, Django's default template engine is **Django Template Language (DTL)**.

Jinja2 is a separate template engine that can also be used with Django.

```text
Django
  └── Default Template Engine
          └── Django Template Language (DTL)

Jinja2
  └── Separate Template Engine
```

> **Note:** The syntax is similar, but Django Template Language and Jinja2 are not identical.

---

# 💻 VS Code Configuration

When working with Django HTML templates, VS Code may recognize the file as normal HTML.

To improve Emmet support:

```text
Ctrl + ,
```

Search for:

```text
Emmet: Include Languages
```

Add:

```json
"emmet.includeLanguages": {
    "django-html": "html"
}
```

You can also select the language mode from the bottom-right corner of VS Code.

Change:

```text
HTML
```

to:

```text
Django HTML
```

This makes working with Django template files more convenient.

---

# 📁 Recommended Project Structure

A basic project can look like this:

```text
myproject/
│
├── manage.py
│
├── myproject/
│   ├── __init__.py
│   ├── settings.py
│   ├── urls.py
│   ├── asgi.py
│   └── wsgi.py
│
└── chai/
    ├── __init__.py
    ├── admin.py
    ├── apps.py
    ├── models.py
    ├── tests.py
    ├── urls.py
    ├── views.py
    │
    ├── migrations/
    │   └── __init__.py
    │
    └── templates/
        └── chai/
            ├── home.html
            ├── about.html
            └── contact.html
```

---

# 🔄 Complete Django Request Flow

Suppose the user visits:

```text
/chai/about/
```

Django processes it like this:

```text
                  Browser
                     │
                     ▼
                /chai/about/
                     │
                     ▼
               project/urls.py
                     │
                     ▼
             include('chai.urls')
                     │
                     ▼
                 chai/urls.py
                     │
                     ▼
                 views.about()
                     │
                     ▼
                  render(...)
                     │
                     ▼
                 about.html
                     │
                     ▼
                  Browser
```

### The Core Architecture

```text
URL
 ↓
URL Configuration
 ↓
View
 ↓
Template
 ↓
Response
```

---

# 🧪 Running the Project

Start the development server:

```bash
py manage.py runserver
```

Then open:

```text
http://127.0.0.1:8000/
```

For the Chai app:

```text
http://127.0.0.1:8000/chai/
```

### Example Pages

```text
/chai/
/chai/about/
/chai/contact/
```

---

# 📚 Useful Django Commands

### Create an app

```bash
py manage.py startapp chai
```

### Start the development server

```bash
py manage.py runserver
```

### Create migrations

```bash
py manage.py makemigrations
```

### Apply migrations

```bash
py manage.py migrate
```

### Create an admin user

```bash
py manage.py createsuperuser
```

---

# 🎯 Learning Goals

By completing this project, you should understand:

- [ ] What a Django project is
- [ ] What a Django app is
- [ ] How to create an app
- [ ] How to register an app
- [ ] How Django URL routing works
- [ ] How `include()` works
- [ ] How views work
- [ ] How templates work
- [ ] Django template syntax
- [ ] Jinja2-style syntax
- [ ] Template inheritance
- [ ] Named URLs
- [ ] Basic VS Code configuration

---

# ⭐ Key Takeaway

The core architecture to remember is:

```text
                  Django Project
                       │
                       ▼
                    urls.py
                       │
                ┌──────┴──────┐
                │             │
             include()    direct path
                │             │
                ▼             ▼
           App urls.py       View
                │
                ▼
               View
                │
                ▼
             Template
                │
                ▼
             Response
                │
                ▼
              Browser
```

> **Django connects URLs to views, views to templates, and templates generate the HTML that the browser displays.**

---

# 📌 Repository Purpose

This repository is intended as a learning reference for understanding the fundamentals of:

- Django apps
- URL routing
- Views
- Templates
- Template inheritance
- Named URLs
- Jinja2/Django template syntax

As the project grows, additional Django concepts such as **models, forms, authentication, static files, databases, and APIs** can be added.

---

## 👩‍💻 Learning Project

Built as a hands-on reference while learning Django fundamentals.

**Keep learning. Keep building. 🚀**
