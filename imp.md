// TAILWIND

 py manage.py tailwind init

 

 
py manage.py tailwind install



python manage.py migrate => then run server { admin panel }


python manage.py createsuperuser

password: gudiya_4567


// admin login

// handle model urls in python

python -m pip install Pillow

python manage.py makemigrations chai




// DJANGO PROJECT

1.py -m venv venv
2. .\venv\Scripts\Activate.ps1
3. pip install django
4. python -m pip install --upgrade pip
5. pip freeze > requirements.txt
6.  django-admin startproject chaicenter
7. cd chaicente
8. ls
9. python manage.py runserver
10. python manage.py makemigrations
11.  python manage.py migrate
12. python manage.py createsuperuser
13. in settings.py :

import os

MEDIA_URL = '/media/'
MEDIA_ROOT = os.path.join(BASE_DIR, 'media')

STATIC_URL= '/static/'
STATICFILES_DIRS = [
    os.path.join(BASE_DIR, 'static'),
]

14. go to urls.py
    from django.conf import settings
from django.conf.urls.static import static

urlpatterns = [
    path('admin/', admin.site.urls),
] + static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)

15. Start app
    python manage.py startapp tweet

16. create urls.py in tweet
17. copy data of urls.py ( of main folder ) to the tweet urls .py { and remove static section }
18. go to views.py
    create a function:
    
def index(request):
    return render(request, 'index.html')


    19. urls.py { of app [ tweet ] }
    from django.urls import path
from .import views

urlpatterns = [
    path('', views.index, name='index'),
] 

20. settings.py => installed app [ add => 'tweet' ] , templates => { 'DIRS': [os.path.join(BASE_DIR, 'templates')], }
21. create template  folder in tweet => file { index.html }
22. in urls.py { main } =>
    from django.contrib import admin
from django.urls import path,include
from django.conf import settings
from django.conf.urls.static import static

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('tweet.urls')),
] + static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)

23. create a template folder in main project { chai center } => create a file [ index.html ]
    // example
     {% load static %}
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@6.0.0-alpha.1/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-B/GM4XqrwHnWXNOWMbloTmrYXZg10cakYGmpfsR/bbzQ6JAJI4ihuyADKLnBgrCe" crossorigin="anonymous">
    <title>
        {% block title %}
        chai aur django
        {% endblock %}</title>
</head>
<body>
    <div class='container'>
      {% block content %}
      {% endblock  %}
    </div>
</body>
</html>


24. in index.html
    {% extends "layout.html" %}

{% block title %}
CHAI AUR TWEET
{% endblock  %}

{% block content %}
<h1>WELCOME TO CHAI'S DJANGO PROJECT </h1>
{% endblock  %}

25. go to tweet models.py
from django.db import models
from django.contrib.auth.models import User

# Create your models here.

class Tweet(models.Model):
    user=models.ForeignKey(User,on_delete=models.CASCADE)
    text=models.TextField(max_length=240)
    photo=models.ImageField(upload_to='photos/',blank=True,null=True)
    created_at=models.DateTimeField(auto_now_add=True)
    updated_at=models.DateTimeField(auto_now=True)

    def __str__(self):
        return f'{self.user.username}-{self.text[:10]}'
26. python -m pip install Pillow
27. pip freeze > requirement.txt
28. python manage.py makemigrations
29. python manage.py migrate
30. register in admin.py
    from django.contrib import admin
from .models import Tweet

# Register your models here.

admin.site.register(Tweet)

31. create new file in tweet { forms.py }
    from django import forms
from .models import Tweet

class TweetForm(forms.ModelForm):
    class Meta:
        model=Tweet
        fields=['text','photo']

   32. go to views.py
       from django.shortcuts import render
from .models import Tweet
from .forms import TweetForm
from django.shortcuts import get_object_or_404,redirect
# Create your views here.

def index(request):
    return render(request, 'index.html')


def tweet_list(request):
    tweets=Tweet.objects.all().order_by('-created_at')
    return render(request,'tweet_list.html',{'tweets':tweets})

def tweet_create(request):
    if request.method=='POST':
      form=TweetForm(request.POST,request.FILES)
      if form.is_valid():
          tweet=form.save(commit=False)
          tweet.user=request.user
          tweet.save()
          return redirect ('tweet_list')
    else:
        form=TweetForm()
    return render(request,'tweet_form.html',{'form':form})


def tweet_edit(request,tweet_id):
    tweet=get_object_or_404(Tweet,pk=tweet_id,user=request.user)
    if request.method=='POST':
      form=TweetForm(request.POST,request.FILES,instance=tweet)
      if form.is_valid():
          tweet=form.save(commit=False)
          tweet.user=request.user
          tweet.save()
          return redirect('tweet_list')
    else:
        form=TweetForm(instance=tweet)
    return render(request,'tweet_form.html',{'form':form})


def tweet_delete(request,tweet_id):
    tweet=get_object_or_404(Tweet,pk=tweet_id,user=request.user)
    if request.method=='POST':
        tweet.delete()
        return redirect('tweet_list')
    return render(request,'tweet_confirm_delete.html',{'tweet':tweet})


    33. three file in templates folder of tweet => tweet_list.html,tweet_form.html,tweet_confirm_delete.html

    34. 

