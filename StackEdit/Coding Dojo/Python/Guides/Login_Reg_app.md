
## Steps to create new Django project/app

##### Note:
* I created this guide for Windows. There are some comments that include Mac/Linux variations. All of the slashes `\` in filepaths will need to be converted to `/` for *nix based systems.
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

### Create login_reg_app
* ___create___ app with `manage.py` _startapp_
```console
(djangoServeEnv) C:\....\django_intro\{project_name}> cd apps
(djangoServeEnv) C:\....\{project_name}\apps> python ..\manage.py startapp login_reg_app
(djangoServeEnv) C:\....\{project_name}\apps> cd login_reg_app
(djangoServeEnv) C:\....\{project_name}\apps\{app_name}> nul>urls.py ## for MAC or LINUX use > touch urls.py
```

### Configure the route to your app
* ___modify___ `INSTALLED_APPS` list in _...\\{project_name}\\{project_name}\settings.py_
```python
INSTALLED_APPS = [
       'apps.login_reg_app', # create this line with your app's name
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
from django.conf.urls import url, include ## add 'include'

urlpatterns = [
url(r'^accounts', include('apps.login_reg_app.urls')),
]
```
* ___add___ app level `urlpatterns` list in _...\\{project_name}\\apps\\{app_name}\\urls.py_
```python
## {project}/apps/login_reg_app/urls.py ##
from django.conf.urls import url
from . import views

urlpatterns = [
url(r'^success', views.success),
url(r'^register/?$', views.register),
url(r'^login/?$', views.login),
url(r'^logout/?$', views.logout),
url(r'^$', views.login_register),
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

### POST Requests / CSRF Tokens
* in each form:
```html
<form  action="/random_word",  method='post'>
{% csrf_token %} 
<input  type="submit"  value="Generate">
</form>
```
### Initialize the database
```console
(djangoServeEnv) C:\....\{project_name}> python manage.py migrate
```

### Messages
* [Adding a message](https://docs.djangoproject.com/en/2.2/ref/contrib/messages/#adding-a-message)
* Displaying messages on template:
```html
{% if messages %}
    <ul  class="messages">
        {% for message in messages %}
            <li{%  if  message.tags  %} class="{{ message.tags }}" {%  endif  %}>{{ message }}</li>
        {% endfor %}
    </ul>
{% endif %}
```

### Passwords
* Hashing
```python
>>> import bcrypt
>>> hash1 = bcrypt.hashpw('test'.encode(), bcrypt.gensalt())
>>> print(hash1)
$2b$12$Wdc2qwiP6u0WdQdKwmer7.DMIcY6q76GxvrJgaodnpRDmpP8mwkDa
```
* validating
```python
def validate_login(request):
    user = User.objects.get(email=request.POST['email'])  # hm...is it really a good idea to use the get method here?
    if bcrypt.checkpw(request.POST['password'].encode(), user.pw_hash.encode()):
        print("password match")
    else:
        print("failed password")
```

<!--stackedit_data:
eyJoaXN0b3J5IjpbNzQwMDgxMTUxXX0=
-->