## Steps to create new Django project/app

##### Note:
* I am using __djangoServEnv__ as my environment name
* Substitute in your own values when the text is contained in curly brackets `{}`
### Set up the project
* ___activate___ environment , create a project
```console
C:\....django\django_intro> djangoServeEnv\Scripts\activate
(djangoServeEnv) C:\....\django\django_intro> pip install django==1.10
(djangoServeEnv) C:\....\django\django_intro> django-admin startproject {project_name}
(djangoServeEnv) C:\....\django\django_intro\> cd your_project_name_here
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
(djangoServeEnv) C:\....\{project_name}\apps> nul>urls.py ## for MAC or LINUX use > touch urls.py
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
from django.conf.urls import url
from . import views
                    
urlpatterns = [
    url(r'^$', views.index),
]
```
* ___add___ app level views in  _...\\{project_name}\\apps\\{app_name}\\views.py_
```python
from django.shortcuts import render, HttpResponse
def index(request):
    return HttpResponse("this is the equivalent of @app.route('/')!")
```
* ___test___ the server again at http://localhost:8000/ 
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE4OTE2NzQ0ODNdfQ==
-->