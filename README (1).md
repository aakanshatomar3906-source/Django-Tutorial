# Django Tutorial --- Beginner to Templates & Static Files

A beginner-friendly Django learning repository covering **Django
installation, virtual environments, project creation, development
server, URL routing, views, templates, dynamic data, template tags,
static files, CSS, and template inheritance**.

This repository is designed as a practical learning guide: understand
the request-response flow, build a simple website, and gradually move
from static HTML to dynamic Django templates.

------------------------------------------------------------------------

## 📚 Table of Contents

-   [About This Repository](#about-this-repository)
-   [What You Will Learn](#what-you-will-learn)
-   [Prerequisites](#prerequisites)
-   [1. Install Django](#1-install-django)
-   [2. Check Django Version](#2-check-django-version)
-   [3. Create a Virtual Environment](#3-create-a-virtual-environment)
-   [4. Activate the Virtual
    Environment](#4-activate-the-virtual-environment)
-   [5. Install Django with uv](#5-install-django-with-uv)
-   [6. Create a Django Project](#6-create-a-django-project)
-   [7. Run the Development Server](#7-run-the-development-server)
-   [8. Django Architecture](#8-django-architecture)
-   [9. Understanding Django
    Templates](#9-understanding-django-templates)
-   [10. Create the Templates Folder](#10-create-the-templates-folder)
-   [11. Configure Templates in
    settings.py](#11-configure-templates-in-settingspy)
-   [12. Create Your First Template](#12-create-your-first-template)
-   [13. Render a Template from
    views.py](#13-render-a-template-from-viewspy)
-   [14. Connect URLs to Views](#14-connect-urls-to-views)
-   [15. Dynamic Data in Templates](#15-dynamic-data-in-templates)
-   [16. Multiple Variables](#16-multiple-variables)
-   [17. If-Else Conditions](#17-if-else-conditions)
-   [18. For Loops](#18-for-loops)
-   [19. Django Template Syntax](#19-django-template-syntax)
-   [20. Static Files](#20-static-files)
-   [21. Configure Static Files](#21-configure-static-files)
-   [22. Connect CSS to HTML](#22-connect-css-to-html)
-   [23. Template Inheritance](#23-template-inheritance)
-   [24. base.html](#24-basehtml)
-   [25. home.html](#25-homehtml)
-   [26. about.html](#26-abouthtml)
-   [27. Final Architecture](#27-final-architecture)
-   [28. Important Django Commands](#28-important-django-commands)
-   [29. Beginner Practice Project](#29-beginner-practice-project)
-   [30. Recommended Learning
    Sequence](#30-recommended-learning-sequence)
-   [31. Common Beginner Mistakes](#31-common-beginner-mistakes)
-   [32. Useful Checklist](#32-useful-checklist)

------------------------------------------------------------------------

## About This Repository

**Django-Tutorial** is a hands-on learning project for understanding the
fundamentals of Django.

The project starts from installation and gradually introduces:

``` text
Python
  ↓
Virtual Environment
  ↓
Django
  ↓
Project
  ↓
URLs
  ↓
Views
  ↓
Templates
  ↓
Dynamic Data
  ↓
Static Files
  ↓
CSS
  ↓
Template Inheritance
```

The goal is not just to memorize commands, but to understand **how
Django processes a browser request and returns a response**.

------------------------------------------------------------------------

## What You Will Learn

By completing this tutorial, you will understand:

-   What Django is
-   How to install Django
-   How to create a virtual environment
-   How to use `uv`
-   How to create a Django project
-   How to start the Django development server
-   How `urls.py` works
-   How `views.py` works
-   What Django templates are
-   How to pass data from views to templates
-   Django template variables
-   Template `if/else`
-   Template `for` loops
-   Django template tags
-   Static CSS, JavaScript, and image files
-   `{% load static %}`
-   `{% static %}`
-   Template inheritance
-   `base.html`
-   `{% extends %}`
-   `{% block %}`
-   Basic Django project architecture

------------------------------------------------------------------------

# 1. Install Django

For Windows, Django can be installed using:

``` powershell
py -m pip install Django==5.2.17
```

You can verify the installation with:

``` powershell
python -m django --version
```

You should see the installed Django version.

> **Note:** If you are using a virtual environment, it is generally
> better to activate it before installing project dependencies so that
> the packages remain isolated to the project.

------------------------------------------------------------------------

# 2. Check Django Version

Run:

``` powershell
python -m django --version
```

Example:

``` text
5.2.17
```

The exact output depends on the version installed in your environment.

------------------------------------------------------------------------

# 3. Create a Virtual Environment

A virtual environment keeps project dependencies isolated.

Instead of installing every Python package globally, each project can
have its own environment.

### Install `uv`

``` powershell
pip install uv
```

### Create a virtual environment

``` powershell
uv venv
```

This creates:

``` text
.venv/
```

inside your project directory.

Typical structure:

``` text
Django/
└── .venv/
```

------------------------------------------------------------------------

# 4. Activate the Virtual Environment

On Windows PowerShell:

``` powershell
.venv\Scripts\activate
```

After activation, your terminal may look similar to:

``` text
(.venv) PS C:\Users\...\Django>
```

The exact environment name can vary depending on how your environment is
configured.

------------------------------------------------------------------------

# 5. Install Django with uv

After activating the virtual environment:

``` powershell
uv pip install Django
```

You can verify Django:

``` powershell
python -m django --version
```

------------------------------------------------------------------------

# 6. Create a Django Project

Create the project:

``` powershell
django-admin startproject AakanshaDjangoProject
```

Move into the project directory:

``` powershell
cd AakanshaDjangoProject
```

A basic Django project will contain something similar to:

``` text
AakanshaDjangoProject/
│
├── manage.py
│
└── AakanshaDjangoProject/
    ├── __init__.py
    ├── settings.py
    ├── urls.py
    ├── asgi.py
    └── wsgi.py
```

### What are these files?

  File            Purpose
  --------------- ---------------------------------------------
  `manage.py`     Command-line utility for the Django project
  `settings.py`   Project configuration
  `urls.py`       URL routing
  `asgi.py`       ASGI entry point
  `wsgi.py`       WSGI entry point
  `__init__.py`   Marks the directory as a Python package

------------------------------------------------------------------------

# 7. Run the Development Server

Inside the folder containing `manage.py`:

``` powershell
python manage.py runserver
```

You should see something similar to:

``` text
Starting development server at http://127.0.0.1:8000/
```

Open:

``` text
http://127.0.0.1:8000/
```

in your browser.

## Run Django on another port

For example:

``` powershell
python manage.py runserver 8001
```

Then open:

``` text
http://127.0.0.1:8001/
```

### Important

Always run `manage.py` commands from the directory where `manage.py`
exists.

For example:

``` text
AakanshaDjangoProject/
├── manage.py
└── AakanshaDjangoProject/
```

Run:

``` powershell
python manage.py runserver
```

from the first `AakanshaDjangoProject/` directory.

------------------------------------------------------------------------

# 8. Django Architecture

A simplified Django request-response flow looks like this:

``` text
Browser
   │
   │ HTTP Request
   ↓
Django
   │
   ↓
URL Resolver
   │
   ↓
urls.py
   │
   ↓
views.py
   │
   │ asks for / saves data
   ↕
models.py
   │
   ↕
Database
   │
   │ data
   ↓
models.py
   ↓
views.py
   │
   │ Response
   ↓
Django
   ↓
Browser
```

## Simple way to remember it

``` text
URL decides
     ↓
View processes
     ↓
Model handles data
     ↓
Database stores data
```

For template-based pages:

``` text
Browser
   ↓
Request
   ↓
urls.py
   ↓
views.py
   ↓
Template (HTML)
   ↓
Response
   ↓
Browser
```

------------------------------------------------------------------------

# 9. Understanding Django Templates

A Django template is basically an HTML file enhanced with Django's
template syntax.

Normal HTML:

``` html
<h1>Hello Aakansha</h1>
```

A dynamic Django template:

``` html
<h1>Hello {{ name }}</h1>
```

If the view sends:

``` python
name = "Aakansha"
```

the browser can display:

``` text
Hello Aakansha
```

Templates are mainly responsible for presenting information to the user.

------------------------------------------------------------------------

# 10. Create the Templates Folder

A project-level templates folder can be created like this:

``` text
AakanshaDjangoProject/
│
├── manage.py
│
├── AakanshaDjangoProject/
│   ├── settings.py
│   ├── urls.py
│   └── ...
│
└── templates/
    └── index.html
```

This is a **project-level templates directory**.

------------------------------------------------------------------------

# 11. Configure Templates in settings.py

Open:

``` text
AakanshaDjangoProject/settings.py
```

Find the `TEMPLATES` configuration.

Usually it looks similar to:

``` python
TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [],
        'APP_DIRS': True,
        ...
    },
]
```

Change `DIRS` to:

``` python
TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [BASE_DIR / 'templates'],
        'APP_DIRS': True,
        ...
    },
]
```

Now Django knows that the project's `templates` directory should also be
searched for HTML templates.

------------------------------------------------------------------------

# 12. Create Your First Template

Create:

``` text
templates/index.html
```

Example:

``` html
<!DOCTYPE html>
<html>
<head>
    <title>My Django Website</title>
</head>

<body>

    <h1>Hello Django</h1>

</body>
</html>
```

------------------------------------------------------------------------

# 13. Render a Template from views.py

Open your `views.py`.

For a simple project-level example:

``` python
from django.shortcuts import render

def home(request):
    return render(request, 'index.html')
```

The following:

``` python
render(request, 'index.html')
```

means that Django should render the `index.html` template and return the
generated HTML response.

------------------------------------------------------------------------

# 14. Connect URLs to Views

Open the project's:

``` text
urls.py
```

Import the views:

``` python
from django.contrib import admin
from django.urls import path
from . import views
```

Then configure:

``` python
urlpatterns = [
    path('admin/', admin.site.urls),
    path('', views.home),
]
```

Now:

``` text
http://127.0.0.1:8000/
```

will call:

``` python
views.home
```

which renders:

``` text
index.html
```

### Complete example

``` python
from django.contrib import admin
from django.urls import path
from . import views

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', views.home),
]
```

------------------------------------------------------------------------

# 15. Dynamic Data in Templates

Now let's send data from the view to the template.

### views.py

``` python
from django.shortcuts import render

def home(request):
    name = "Aakansha"

    return render(request, 'index.html', {
        'name': name
    })
```

### index.html

``` html
<h1>Hello {{ name }}</h1>
```

### Browser output

``` text
Hello Aakansha
```

The syntax:

``` django
{{ name }}
```

is used to display a template variable.

------------------------------------------------------------------------

# 16. Multiple Variables

### views.py

``` python
from django.shortcuts import render

def home(request):

    name = "Aakansha"
    age = 20
    city = "Meerut"

    return render(request, 'index.html', {
        'name': name,
        'age': age,
        'city': city
    })
```

### index.html

``` html
<h1>Name: {{ name }}</h1>
<p>Age: {{ age }}</p>
<p>City: {{ city }}</p>
```

The dictionary passed to `render()` is called the **context**.

Conceptually:

``` text
View
 │
 │ context
 ↓
Template
 │
 ↓
HTML
```

------------------------------------------------------------------------

# 17. If-Else Conditions

Django templates support conditional logic.

``` django
{% if name %}
    <h1>Hello {{ name }}</h1>
{% else %}
    <h1>Hello Guest</h1>
{% endif %}
```

Basic syntax:

``` django
{% if condition %}

{% else %}

{% endif %}
```

Remember:

-   `{{ }}` → display a value
-   `{% %}` → execute a template tag/control structure

------------------------------------------------------------------------

# 18. For Loops

Suppose the view contains a list:

### views.py

``` python
from django.shortcuts import render

def home(request):

    fruits = ["Apple", "Mango", "Banana", "Orange"]

    return render(request, 'index.html', {
        'fruits': fruits
    })
```

### index.html

``` html
<h2>Fruits</h2>

<ul>
    {% for fruit in fruits %}
        <li>{{ fruit }}</li>
    {% endfor %}
</ul>
```

Output:

``` text
Fruits

- Apple
- Mango
- Banana
- Orange
```

General loop syntax:

``` django
{% for item in items %}
    {{ item }}
{% endfor %}
```

------------------------------------------------------------------------

# 19. Django Template Syntax

There are three major syntax patterns to remember.

## 19.1 Variable

``` django
{{ name }}
```

Used to display data.

------------------------------------------------------------------------

## 19.2 Tag

``` django
{% if name %}
```

Used for logic, loops, loading static files, inheritance, and other
template operations.

------------------------------------------------------------------------

## 19.3 Comment

Single-line comment:

``` django
{# This is a Django comment #}
```

Multi-line comment:

``` django
{% comment %}
This is a multi-line comment.
{% endcomment %}
```

### Quick reference

  Syntax             Purpose
  ------------------ ------------------------------
  `{{ variable }}`   Display data
  `{% tag %}`        Template logic/instructions
  `{# comment #}`    Single-line template comment
  `{% comment %}`    Multi-line template comment

------------------------------------------------------------------------

# 20. Static Files --- CSS, JavaScript, Images

Static files are files such as:

-   CSS
-   JavaScript
-   Images
-   Fonts
-   Other front-end assets

A simple project structure:

``` text
AakanshaDjangoProject/
│
├── static/
│   ├── css/
│   │   └── style.css
│   ├── js/
│   │   └── script.js
│   └── images/
│       └── logo.png
│
└── templates/
    └── index.html
```

------------------------------------------------------------------------

# 21. Configure Static Files

In `settings.py`:

``` python
STATIC_URL = 'static/'
```

For a project-level `static` folder, add:

``` python
STATICFILES_DIRS = [
    BASE_DIR / 'static',
]
```

Example:

``` python
STATIC_URL = 'static/'

STATICFILES_DIRS = [
    BASE_DIR / 'static',
]
```

This tells Django where to find additional static files during
development.

------------------------------------------------------------------------

# 22. Connect CSS to HTML

At the top of the template, load Django's static template tag:

``` django
{% load static %}
```

Then connect your CSS:

``` html
<link rel="stylesheet" href="{% static 'css/style.css' %}">
```

### Complete example

``` html
{% load static %}

<!DOCTYPE html>
<html>
<head>
    <title>Django</title>

    <link rel="stylesheet" href="{% static 'css/style.css' %}">
</head>

<body>

    <h1>Hello Django</h1>

</body>
</html>
```

If your file is:

``` text
static/css/style.css
```

the correct reference is:

``` django
{% static 'css/style.css' %}
```

If your file is directly inside:

``` text
static/style.css
```

use:

``` django
{% static 'style.css' %}
```

### Important rule

The path inside `{% static %}` is relative to the `static` directory.

``` text
static/
└── css/
    └── style.css
```

Therefore:

``` django
{% static 'css/style.css' %}
```

------------------------------------------------------------------------

# 23. Template Inheritance

Template inheritance is one of Django's most useful features.

Imagine every page has the same:

-   Navbar
-   Footer
-   CSS
-   Basic HTML structure

Instead of repeating that code on every page, create a common parent
template.

Example:

``` text
templates/
│
├── base.html
├── home.html
└── about.html
```

The child templates can reuse `base.html`.

------------------------------------------------------------------------

# 24. base.html

Example:

``` html
{% load static %}

<!DOCTYPE html>
<html>
<head>

    <title>{% block title %}My Website{% endblock %}</title>

    <link rel="stylesheet" href="{% static 'css/style.css' %}">

</head>

<body>

    <nav>
        <a href="/">Home</a>
        <a href="/about/">About</a>
    </nav>

    {% block content %}
    {% endblock %}

    <footer>
        <p>My Website</p>
    </footer>

</body>
</html>
```

This:

``` django
{% block content %}
{% endblock %}
```

creates a placeholder where child templates can insert their content.

Similarly:

``` django
{% block title %}
{% endblock %}
```

allows child templates to customize the page title.

------------------------------------------------------------------------

# 25. home.html

``` django
{% extends 'base.html' %}

{% block title %}
Home
{% endblock %}

{% block content %}

<h1>Welcome to Home Page</h1>

<p>This is my Django website.</p>

{% endblock %}
```

The line:

``` django
{% extends 'base.html' %}
```

tells Django that `home.html` inherits from `base.html`.

------------------------------------------------------------------------

# 26. about.html

``` django
{% extends 'base.html' %}

{% block title %}
About
{% endblock %}

{% block content %}

<h1>About Us</h1>

<p>This is the about page.</p>

{% endblock %}
```

Both `home.html` and `about.html` reuse the common structure from
`base.html`.

------------------------------------------------------------------------

# 27. Final Architecture

## Basic template flow

``` text
                 Browser
                    │
                    │ Request
                    ↓
                 urls.py
                    │
                    ↓
                 views.py
                    │
                    │ context/data
                    ↓
                Template
                (HTML file)
                    │
                    ↓
              HTML Response
                    │
                    ↓
                 Browser
```

## With database

``` text
                 Browser
                    │
                  Request
                    ↓
                 urls.py
                    ↓
                 views.py
                  ↕     │
                  │     │ context
                  │     ↓
                  │  Template
                  │     │
                  │     ↓
                  │ HTML Response
                  │
                  ↕
               models.py
                  ↕
               Database
```

## Easy mental model

``` text
URL
 ↓
View
 ↓
Model / Database
 ↓
Context
 ↓
Template
 ↓
HTML
 ↓
Browser
```

Or simply:

``` text
urls.py    → URL decides where the request goes
views.py   → Application logic
models.py  → Database/data layer
template   → HTML/UI
database   → Stores application data
```

------------------------------------------------------------------------

# 28. Important Django Commands

## Create a project

``` powershell
django-admin startproject AakanshaDjangoProject
```

## Enter project directory

``` powershell
cd AakanshaDjangoProject
```

## Start development server

``` powershell
python manage.py runserver
```

## Start server on another port

``` powershell
python manage.py runserver 8001
```

## Create an application

``` powershell
python manage.py startapp myapp
```

## Check Django version

``` powershell
python -m django --version
```

## Create migrations

``` powershell
python manage.py makemigrations
```

## Apply migrations

``` powershell
python manage.py migrate
```

## Find a static file

``` powershell
python manage.py findstatic css/style.css
```

This is useful when troubleshooting static-file configuration.

------------------------------------------------------------------------

# 29. Beginner Practice Project

After learning the concepts above, build a small website with:

``` text
Django Website
│
├── Home Page
├── About Page
├── Contact Page
└── CSS
```

Suggested URL structure:

``` text
/          → home()
/about/    → about()
/contact/  → contact()
```

Architecture:

``` text
                    urls.py
                       │
          ┌────────────┼────────────┐
          ↓            ↓            ↓
       home()       about()      contact()
          │            │            │
          └────────────┼────────────┘
                       ↓
                    Templates
                       │
                       ↓
                      HTML
                       │
                       ↓
                      CSS
                       │
                       ↓
                    Browser
```

## Suggested practice progression

### Level 1 --- Static page

Create:

``` text
home.html
```

with basic HTML.

### Level 2 --- View

Create:

``` python
def home(request):
    return render(request, 'home.html')
```

### Level 3 --- URL

Connect the view:

``` python
path('', views.home)
```

### Level 4 --- Dynamic data

Pass:

``` python
{
    'name': 'Aakansha'
}
```

and display:

``` django
{{ name }}
```

### Level 5 --- Conditions

Use:

``` django
{% if %}
{% else %}
{% endif %}
```

### Level 6 --- Loops

Use:

``` django
{% for %}
{% endfor %}
```

### Level 7 --- CSS

Create:

``` text
static/css/style.css
```

and connect it with:

``` django
{% load static %}
```

### Level 8 --- Template inheritance

Create:

``` text
base.html
home.html
about.html
```

and use:

``` django
{% extends 'base.html' %}
```

------------------------------------------------------------------------

# 30. Recommended Learning Sequence

Do not try to memorize Django all at once.

Follow this order:

``` text
1. Python basics
       ↓
2. Virtual environments
       ↓
3. Django installation
       ↓
4. Django project
       ↓
5. runserver
       ↓
6. urls.py
       ↓
7. views.py
       ↓
8. Templates
       ↓
9. Context / Dynamic Data
       ↓
10. if / else
       ↓
11. for loops
       ↓
12. Static Files
       ↓
13. CSS
       ↓
14. Template Inheritance
       ↓
15. Django Apps
       ↓
16. Models
       ↓
17. Database
       ↓
18. Forms
       ↓
19. Authentication
       ↓
20. APIs / Django REST Framework
```

For this repository, focus primarily on **steps 1--14** before moving
into database-heavy Django development.

------------------------------------------------------------------------

# 31. Common Beginner Mistakes

## 1. Running `manage.py` from the wrong directory

If you get:

``` text
can't open file '...manage.py':
[Errno 2] No such file or directory
```

you are probably not inside the directory containing `manage.py`.

Check:

``` powershell
dir
```

Then navigate into the correct folder:

``` powershell
cd AakanshaDjangoProject
```

------------------------------------------------------------------------

## 2. Forgetting `{% load static %}`

If using:

``` django
{% static 'css/style.css' %}
```

make sure the template has:

``` django
{% load static %}
```

near the top.

------------------------------------------------------------------------

## 3. Incorrect static path

If your file is:

``` text
static/css/style.css
```

use:

``` django
{% static 'css/style.css' %}
```

Not:

``` django
{% static 'static/css/style.css' %}
```

------------------------------------------------------------------------

## 4. Wrong `STATICFILES_DIRS`

For a project-level static directory:

``` python
STATICFILES_DIRS = [
    BASE_DIR / 'static',
]
```

------------------------------------------------------------------------

## 5. Forgetting to save files

After changing:

-   `settings.py`
-   `urls.py`
-   `views.py`
-   `index.html`
-   `style.css`

save the file before testing.

For CSS changes, a hard browser refresh can help:

``` text
Ctrl + Shift + R
```

------------------------------------------------------------------------

## 6. Running the command outside the virtual environment

Check that your environment is activated before installing or running
project dependencies.

Example:

``` text
(.venv) PS C:\...\Django>
```

------------------------------------------------------------------------

# 32. Useful Checklist

## Environment

-   [ ] Python installed
-   [ ] Virtual environment created
-   [ ] Virtual environment activated
-   [ ] Django installed
-   [ ] Django version checked

## Project

-   [ ] Django project created
-   [ ] `manage.py` understood
-   [ ] Development server started
-   [ ] Browser opened at `127.0.0.1:8000`

## Templates

-   [ ] `templates/` folder created
-   [ ] `settings.py` configured
-   [ ] `index.html` created
-   [ ] View created
-   [ ] URL connected
-   [ ] Template rendered

## Dynamic Data

-   [ ] Context understood
-   [ ] Variables used
-   [ ] `if/else` practiced
-   [ ] `for` loop practiced

## Static Files

-   [ ] `static/` folder created
-   [ ] `STATIC_URL` configured
-   [ ] `STATICFILES_DIRS` configured
-   [ ] `{% load static %}` understood
-   [ ] CSS connected
-   [ ] `findstatic` command tested

## Template Inheritance

-   [ ] `base.html` created
-   [ ] `{% block %}` understood
-   [ ] `{% extends %}` understood
-   [ ] `home.html` created
-   [ ] `about.html` created

------------------------------------------------------------------------

# 🧠 Quick Revision

### Django project

``` powershell
django-admin startproject AakanshaDjangoProject
```

### Start server

``` powershell
python manage.py runserver
```

### URL

``` python
path('', views.home)
```

### View

``` python
def home(request):
    return render(request, 'index.html')
```

### Template variable

``` django
{{ name }}
```

### Condition

``` django
{% if name %}
    Hello {{ name }}
{% endif %}
```

### Loop

``` django
{% for item in items %}
    {{ item }}
{% endfor %}
```

### Static files

``` django
{% load static %}
```

``` django
<link rel="stylesheet" href="{% static 'css/style.css' %}">
```

### Template inheritance

``` django
{% extends 'base.html' %}
```

``` django
{% block content %}
{% endblock %}
```

------------------------------------------------------------------------

# 🎯 Final Mental Model

When a user opens a Django URL:

``` text
Browser
   │
   │ HTTP Request
   ↓
urls.py
   │
   │ finds the correct route
   ↓
views.py
   │
   │ processes the request
   │
   ├──────────────→ models.py → Database
   │
   ↓
Context / Data
   │
   ↓
Template
   │
   │ HTML + CSS
   ↓
HTTP Response
   │
   ↓
Browser
```

### Remember this:

> **URL decides → View processes → Model handles data → Template
> presents → Browser displays**

This mental model will make it much easier to understand the rest of
Django as you progress toward apps, models, databases, forms,
authentication, and APIs.

------------------------------------------------------------------------

## 🚀 Next Steps

After completing this tutorial, continue with:

1.  Django Applications
2.  Models and Database
3.  Django ORM
4.  Migrations
5.  Django Admin
6.  Forms
7.  CRUD Operations
8.  User Authentication
9.  Django REST Framework
10. Building a complete Django project

------------------------------------------------------------------------

## 📌 Repository Goal

This repository is a learning record of my journey through Django and
web development.

The focus is on **learning by building, understanding the architecture,
writing code, debugging errors, and gradually developing complete web
applications.**

**Keep building. Keep debugging. Keep learning. 🚀**
