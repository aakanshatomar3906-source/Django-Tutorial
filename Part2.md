Jinja2 & Django Apps

A beginner-friendly Django project demonstrating how to create Django apps, configure URL routing, connect views, and work with Django/Jinja-style templates.

📌 Project Overview

This project is created to understand the basic structure of a Django application and how different components communicate with each other.

The main concepts covered are:

Creating a Django app

Registering an app in INSTALLED_APPS

Creating and connecting urls.py

Creating Django views

Using include() for app-level URL routing

Working with Django HTML templates

Understanding Jinja2-style template syntax

Configuring Emmet for Django HTML in VS Code

Understanding the flow:

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

🛠️ Technologies Used

Python

Django

Django Template Language (DTL)

Jinja2 concepts

HTML

VS Code

🚀 Getting Started
1. Create a Django Project

Create a new Django project:

django-admin startproject myproject


Move into the project directory:

cd myproject


Run the development server:

py manage.py runserver


The application will normally be available at:

http://127.0.0.1:8000/

📦 Creating a Django App

Create an app named chai:

py manage.py startapp chai


This creates a structure similar to:

chai/
├── __init__.py
├── admin.py
├── apps.py
├── migrations/
│   └── __init__.py
├── models.py
├── tests.py
└── views.py


A Django project represents the complete website/application, while an app represents a specific feature or module.

For example:

Project
│
├── chai       → Chai-related functionality
├── accounts   → Authentication
├── products   → Products
└── blog       → Blog

⚙️ Register the App

Open:

myproject/settings.py


Add chai to INSTALLED_APPS:

INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',

    'chai',
]


This tells Django that the chai application is part of the project.

🔗 URL Routing

Django uses URL configurations to decide which view should handle a request.

There are generally two levels of URL configuration:

Project URLs
     ↓
App URLs
     ↓
View

Main urls.py

The project's main urls.py can contain:

from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('chai/', include('chai.urls')),
]


The important part is:

path('chai/', include('chai.urls')),


This tells Django:

Any URL beginning with /chai/ should be handled by chai/urls.py.

🧭 App-Level urls.py

Django does not automatically create urls.py when creating an app.

Create it manually:

chai/
├── views.py
├── models.py
├── admin.py
├── apps.py
└── urls.py


Add:

from django.urls import path
from . import views

urlpatterns = [
    path('', views.home, name='home'),
    path('about/', views.about, name='about'),
    path('contact/', views.contact, name='contact'),
]

👀 Views

Open:

chai/views.py


Example:

from django.http import HttpResponse


def home(request):
    return HttpResponse("Welcome to Chai!")


def about(request):
    return HttpResponse("About Chai")


def contact(request):
    return HttpResponse("Contact Chai")


A view receives an HTTP request and returns an HTTP response.

For example:

def home(request):
    return HttpResponse("Welcome to Chai!")


The flow is:

/chai/
   ↓
views.home()
   ↓
"Welcome to Chai!"

🔍 Understanding include()

Suppose the main project has:

path('chai/', include('chai.urls')),


And chai/urls.py contains:

path('menu/', views.menu, name='menu'),


Django combines them:

/chai/ + menu/


Result:

/chai/menu/


So the request flow becomes:

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

🏷️ Named URLs

URLs can be given names:

path('about/', views.about, name='about'),


The name:

about


can be used inside templates:

<a href="{% url 'about' %}">About</a>


This is better than hard-coding:

<a href="/chai/about/">About</a>


Named URLs make applications easier to maintain.

🎨 Django Templates

Instead of returning plain text:

return HttpResponse("Welcome to Chai!")


we can render an HTML template.

Use:

from django.shortcuts import render


def home(request):
    return render(request, 'chai/home.html')


Recommended template structure:

chai/
└── templates/
    └── chai/
        ├── home.html
        ├── about.html
        └── contact.html


Example home.html:

<!DOCTYPE html>
<html>
<head>
    <title>Chai Home</title>
</head>

<body>

    <h1>Welcome to Chai!</h1>

</body>
</html>

🧩 Template Syntax

Django templates use special syntax.

Variables
<h1>{{ name }}</h1>


If the view sends:

return render(
    request,
    'chai/home.html',
    {'name': 'Masala Chai'}
)


the template can display:

Masala Chai

Conditions
{% if user %}
    <p>Welcome!</p>
{% else %}
    <p>Please log in.</p>
{% endif %}

Loops
{% for chai in chais %}
    <p>{{ chai }}</p>
{% endfor %}

URL Tags
<a href="{% url 'home' %}">Home</a>

Comments

Django template comments can be written as:

{# This is a template comment #}


For multiple lines:

{% comment %}
This is a multi-line comment.
{% endcomment %}

🧱 Template Inheritance

One of the most useful Django template features is template inheritance.

Create:

templates/
└── base.html


Example:

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


Then another template can extend it:

{% extends "base.html" %}

{% block title %}
Home
{% endblock %}

{% block content %}

<h1>Welcome to Chai!</h1>

{% endblock %}


This avoids repeating the same HTML on every page.

🟢 Jinja2 vs Django Templates

Jinja2 and Django Template Language have very similar syntax.

Variable
{{ name }}

Condition
{% if user %}
    Hello {{ user }}
{% endif %}

Loop
{% for item in items %}
    {{ item }}
{% endfor %}


However, Django's default template engine is Django Template Language (DTL).

Jinja2 is a separate template engine that can also be used with Django.

Therefore:

Django
  └── Default Template Engine
          └── Django Template Language (DTL)

Jinja2
  └── Separate Template Engine


The syntax is similar, but they are not identical.

💻 VS Code Configuration

When working with Django HTML templates, VS Code may recognize the file as normal HTML.

To improve Emmet support:

Ctrl + ,


Search for:

Emmet: Include Languages


Add:

"emmet.includeLanguages": {
    "django-html": "html"
}


You can also select the language mode from the bottom-right corner of VS Code:

HTML


Change it to:

Django HTML


This makes working with Django template files more convenient.

📁 Recommended Project Structure

A basic project can look like this:

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

🔄 Complete Django Request Flow

Suppose the user visits:

/chai/about/


Django processes it like this:

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


The most important concept is:

URL
 ↓
URL Configuration
 ↓
View
 ↓
Template
 ↓
Response

🧪 Running the Project

Start the development server:

py manage.py runserver


Then open:

http://127.0.0.1:8000/


For the Chai app:

http://127.0.0.1:8000/chai/


Example pages:

/chai/
/chai/about/
/chai/contact/

📚 Useful Django Commands

Create an app:

py manage.py startapp chai


Start the development server:

py manage.py runserver


Create migrations:

py manage.py makemigrations


Apply migrations:

py manage.py migrate


Create an admin user:

py manage.py createsuperuser

🎯 Learning Goals

By completing this project, you should understand:

 What a Django project is

 What a Django app is

 How to create an app

 How to register an app

 How Django URL routing works

 How include() works

 How views work

 How templates work

 Django template syntax

 Jinja2-style syntax

 Template inheritance

 Named URLs

 Basic VS Code configuration

⭐ Key Takeaway

The core architecture to remember is:

                 Django Project
                      │
                      ▼
                  urls.py
                      │
              ┌───────┴───────┐
              │               │
           include()       direct path
              │               │
              ▼               ▼
         App urls.py        View
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


Django connects URLs to views, views to templates, and templates generate the HTML that the browser displays.

📌 Repository Purpose

This repository is intended as a learning reference for understanding the fundamentals of Django apps, URL routing, views, templates, and Jinja2/Django template syntax.

As the project grows, additional Django concepts such as models, forms, authentication, static files, databases, and APIs can be added.
 
