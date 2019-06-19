# Steps to create new Django project/app

##### Note:
* I created this guide for Windows. There are some comments that include Mac/Linux variations. All of the slashes `\` in filepaths will need to be converted to `/` for *nix based systems.
* I am using __djangoServEnv__ as my environment name
* Substitute in your own values when the text is contained in curly brackets `{}`
* Console commands are proceeded with the current path and activated environment
## Set up the project
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

## Create first app
* ___create___ app with `manage.py` _startapp_
```console
(djangoServeEnv) C:\....\django_intro\{project_name}> cd apps
(djangoServeEnv) C:\....\{project_name}\apps> python ..\manage.py startapp {app_name}
(djangoServeEnv) C:\....\{project_name}\apps> cd {app_name}
(djangoServeEnv) C:\....\{project_name}\apps\{app_name}> nul>urls.py ## for MAC or LINUX use > touch urls.py
```

## Configure the route to your app
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
## Project Structure
<img src="https://s3.amazonaws.com/General_V88/boomyeah2015/codingdojo/curriculum/content/chapter/djangoStructure_04.PNG" width="200" height="300" />`

## Link CSS and JS files to html
##### Note: I am calling my css file `styles.css`
```html
<head>
    {% load static %}
    <link rel="stylesheet" href="{% static 'app_name/css/styles.css' %}">
    <script src="{% static 'app_name/js/script.js' %}"></script>
</head>
```

## POST Requests / CSRF Tokens
* in each form:
```html
<form  action="/random_word",  method='post'>
{% csrf_token %} 
<input  type="submit"  value="Generate">
</form>
```
## Initialize the database
```console
(djangoServeEnv) C:\....\{project_name}> python manage.py makemigrations
(djangoServeEnv) C:\....\{project_name}> python manage.py migrate
```

## Messages
* [Adding a message](https://docs.djangoproject.com/en/2.2/ref/contrib/messages/#adding-a-message)
* Displaying messages on template:
#### in views:
```python
from django.contrib import messages
messages.success(request, 'your message here')
errors = Book.objects.validate_add_book(request.POST)
    if len(errors) > 0:
        for key, value in errors.items():
            messages.error(request, value)

        return redirect('/books/')
```
#### in template:
```html
{% if messages %}
    <ul  class="messages">
        {% for message in messages %}
            <li{%  if  message.tags  %} class="{{ message.tags }}" {%  endif  %}>{{ message }}</li>
        {% endfor %}
    </ul>
{% endif %}
```

## Passwords
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
## Project level template extension
C:.
│   db.sqlite3
│   manage.py
│
├───.vscode
│       settings.json
│
├───apps
│   ├───fav_books_app
│   │   │   admin.py
│   │   │   apps.py
│   │   │   models.py
│   │   │   tests.py
│   │   │   urls.py
│   │   │   views.py
│   │   │   __init__.py
│   │   │
│   │   ├───migrations
│   │   │   │   0001_initial.py
│   │   │   │   0002_auto_20190619_0853.py
│   │   │   │   __init__.py
│   │   │   │
│   │   │   └───__pycache__
│   │   │           0001_initial.cpython-37.pyc
│   │   │           0002_auto_20190619_0853.cpython-37.pyc
│   │   │           __init__.cpython-37.pyc
│   │   │
│   │   ├───templates
│   │   │   └───fav_books_app
│   │   │           book.html
│   │   │           book_view.html
│   │   │
│   │   └───__pycache__
│   │           admin.cpython-37.pyc
│   │           models.cpython-37.pyc
│   │           urls.cpython-37.pyc
│   │           views.cpython-37.pyc
│   │           __init__.cpython-37.pyc
│   │
│   └───login_reg_app
│       │   admin.py
│       │   apps.py
│       │   functions.py
│       │   models.py
│       │   tests.py
│       │   urls.py
│       │   views.py
│       │   __init__.py
│       │
│       ├───migrations
│       │   │   0001_initial.py
│       │   │   0002_auto_20190619_0853.py
│       │   │   __init__.py
│       │   │
│       │   └───__pycache__
│       │           0001_initial.cpython-37.pyc
│       │           0002_auto_20190619_0853.cpython-37.pyc
│       │           __init__.cpython-37.pyc
│       │
│       ├───static
│       │   └───login_reg_app
│       │       └───css
│       │               log_reg_styles.css
│       │
│       ├───templates
│       │   └───login_reg_app
│       │           login_register.html
│       │
│       └───__pycache__
│               admin.cpython-37.pyc
│               functions.cpython-37.pyc
│               models.cpython-37.pyc
│               urls.cpython-37.pyc
│               views.cpython-37.pyc
│               __init__.cpython-37.pyc
│
├───favorite_books
│   │   settings.py
│   │   urls.py
│   │   wsgi.py
│   │   __init__.py
│   │
│   └───__pycache__
│           settings.cpython-37.pyc
│           urls.cpython-37.pyc
│           wsgi.cpython-37.pyc
│           __init__.cpython-37.pyc
│
├───static
│   └───css
│           base_styles.css
│           log_reg_styles.css
│
└───templates
        base.html

_project level settings.py_
```python
TEMPLATES = [
		{
	'BACKEND': 'django.template.backends.django.DjangoTemplates',
	'DIRS': [os.path.join(BASE_DIR, 'templates')],
	'APP_DIRS': True,
		'django.contrib.messages.context_processors.messages',
				],
			},
		},
]
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTU3NTE2NzU0OSwtMTQwNzQ2NjI5OCwxOD
ExNjIyNDY2LC0xNjQ4NDcyMTA2LC0xNTQyMDEzMzk2XX0=
-->