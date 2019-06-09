## Steps to create new Django project/app

##### Note:
* I am using __djangoServEnv__ as my environment name
* Substitute in your own values when the text is contained in curly brackets `{}`
* Console commands are proceeded with the current path and activated environment
### Set up the project
* ___activate___ environment , create a project
```console
C:\....django\django_intro> djangoServeEnv\Scripts\activate
(djangoServeEnv) C:\....\django\django_intro> pip install django==1.10
(djangoServeEnv) C:\....\django\django_intro> django-admin startproject {project_name}
(djangoServeEnv) C:\....\django\django_intro\> cd {project_name}
(djangoServeEnv) C:\....\django_intro\{project_name}> python manage.py runserver
```
* ___test___ the server at http://localhost:8000/ 
* _ctrl/cmd + c_ to shutdown the server
* ___create___ apps folder
```console
(djangoServeEnv) C:\....\django_intro\{project_name}> mkdir apps
```

### Create first app
* ___create___ app with `manage.py` _startapp_
```console
(djangoServeEnv) C:\....\django_intro\{project_name}> cd apps
(djangoServeEnv) C:\....\{project_name}\apps> python ..\manage.py startapp {app_name}
(djangoServeEnv) C:\....\{project_name}\apps> cd {app_name}
(djangoServeEnv) C:\....\{project_name}\apps\{app_name}> nul>urls.py ## for MAC or LINUX use > touch urls.py
```

### Configure the route to your app
* ___modify___ `INSTALLED_APPS` list in _...\\{project_name}\\{project_name}\settings.py_
```python
INSTALLED_APPS = [
       'apps.{your_app_name_here}', # create this line with your app's name
       'django.contrib.admin',
       'django.contrib.auth',
       'django.contrib.contenttypes',
       'django.contrib.sessions',
       'django.contrib.messages',
       'django.contrib.staticfiles',
   ]
```
* ___modify___ project level `urlpatterns` list in _...\\{project_name}\\{project_name}\urls.py_
```python 
from django.conf.urls import url, include			# add include
# from django.contrib import admin             			# comment out, or just delete
urlpatterns = [
    url(r'^', include('apps.{your_app_name_here}.urls')),	# use your app name here
    # url(r'^admin/', admin.sites.urls)         		# comment out, or just delete
]
```
* ___add___ app level `urlpatterns` list in _...\\{project_name}\\apps\\{app_name}\\urls.py_
```python
## {app_name} ##
from django.conf.urls import url
from . import views
                    
urlpatterns = [
    url(r'^$', views.index),
]
```
* ___add___ app level views in  _...\\{project_name}\\apps\\{app_name}\\views.py_
```python
## {app name} ##
from django.shortcuts import render, HttpResponse
def index(request):
    return HttpResponse("this is the equivalent of @app.route('/')!")
```
* ___test___ the server again at http://localhost:8000/ 
```console
(djangoServeEnv) C:\....\{project_name}\apps\{app_name}> cd ..\..
(djangoServeEnv) C:\....\{project_name}> python manage.py runserver
```
### Project Structure
<img src="https://s3.amazonaws.com/General_V88/boomyeah2015/codingdojo/curriculum/content/chapter/djangoStructure_04.PNG" width="200" height="300" />`

### Link CSS and JS files to html
##### Note: I am calling my css file `styles.css`
```html
<head>
    {% load static %}
    <link rel="stylesheet" href="{% static 'app_name/css/styles.css' %}">
    <script src="{% static 'app_name/js/script.js' %}"></script>
</head>
```

### CSRF Tokens

### S
<!--stackedit_data:
eyJoaXN0b3J5IjpbODI1MzE2ODkyLDM1NzUyMDE4NSwyMTE3MT
k2MDMzLDc2NzcxMjg2OSw4MDQ5NjIxODgsNDA4MTY2NzYxLDE1
Mzk5MzM0MTYsMjA3MjUyNTQ4NywtNjAxODgzMjE2LC0xOTE4NT
k0NDI5XX0=
-->