# Purpose: Reminder myself how to get started with a PY project.

To run my PY Django project, first ensure below steps in order:
1. Activate a Virtual Environment
2. Check dependencies installed - Django, bcrypt, etc.
3. Run project


* Below common error is caused by missing Django
    * ensure that virtual environment is activated
    * python.pythonpath is correctly hooked up
    * ensure that Django is installed
    ``` python
    ImportError(
                "Couldn't import Django. Are you sure it's installed and "  
                "available on your PYTHONPATH environment variable? Did you "
                "forget to activate a virtual environment?"
            ) from exc
    ```



## Virtual Environment
1. The `venv` module starting from Python 3.3 provides support for creating lightweight "virtual environments" with their own directoies, optionally isolated from system site directories.  
2. Each vEnv has its own Python binary (matches the version of the binary that was used to create this vEnv) and can have its own independent set of installed python packages in its site directories.  
> [`venv` - Creation of Virtual Environments](https://docs.python.org/3/library/venv.html)

- create

    To create new Python Virtual Env with name `vePy3` or `veDjango`, first arrive at the folder directory that will house the PY Virtual Environment (vEnv):
    ```python
    python3 -m venv  vePy3      # -m means module
    python3 -m venv  veDjango
    ```

- activate

    Arrive at the vEnv folder directory:
    ```python
    source vePy3/bin/activate
    source veDjango/bin/activate
    ```

- deactivate
    
    (exiting out of Terninal completely will also deactivate current vEnv)
    ```python
    deactivate
    ```


## Dependencies 

- check
    - current py version installed
        ```
        python3 --version    or    python3 -V  (V must be capital)
        ```
    - list all Python Packages installed
        ```
        pip3 list
        ```

- create

    create a requirements list for dependencies installed specifically for the project
    ```
    pip freeze > requirements.txt
    ```


- install

    - Python

        Access [Python website](https://www.python.org) and install the macOS version  
        [Python Commands](https://docs.python.org/3/using/cmdline.html)

    - pip

        (included with Python installation by default )  
        ```python
        python3 -m pip install --upgrade pip    # to upgrade pip3  ( -m means module )
        ```
    
    - Django

        installing for the vEnv in use, first activate vEnv
        ```python
        pip install Django==2.2 
        ```
    - bcrypt

        installing for the vEnv in use, first activate vEnv
        ```python
        pip install bcrypt
        ```
    
    - project requirements list (dependencies) 
        ```python
        pip install -r requirements.txt
        ```

        \*** Note that within the Python 3 virtual environment, you can use the command python instead of python3, and pip instead of pip3

## Execute PY Project

- run

    arrive in project directory
    ```
    python manage.py runserver
    ```

- stop - `cltr-C`


## Migration

- Session
    
    first activate vEnv; run inside project
    ```python
    python manage.py migrate
    ```

- Model Creation
    
    first activate vEnv; run inside project
    ```python
    python manage.py makemigrations
    python manage.py migrate 
    ```

- Model Corruption

    To delete DB and start from scratch due to corruption, delete 3 files:
    - db.sqlite3 (shut down if db browser is opened)
    - appName/migrations folder
    - appName/__pycache__

    run migration again including appName:
    ```python
    python manage.py makemigrations appName
    python manage.py migrate
    ```

## Run Django Shell/ORM

- activate Django Shell to interact with models in Django ORM
- to view data in sqlite3
    ```python
    python manage.py shell
    from appName.models import *
    ```

- example to retrieve data in Django Shell
    ```python
    tableClassName.objects.all()   
    tableClassName.objects.filter(id=xx).first().delele()
    tableClassName.objects.all()
    ```



## Run PY Interpreter 

- activate PY shell
    ```
    python
    ``` 
    ```
    python3
    ```

- running a PY file
    ```
    python3 <pyFilenameYouWantToRun.py>
    ```

- exit PY shell
    ```
    exit()
    ```

---
## Start and Run a Django Framework Web Server @ Terminal

### **Django** is a Python framework to run a Web Server

* Resolves/Routes URLs (requests) to functions (in views.py = controller) to templates (html pages)
* Handles HTTP request
* Server listens to URL being requested
* Server sends the appropriate responses
* Route => “/“ section in URLs
* Main website route includes first slash:
    * 127.0.0.1:8000/        (_*Flask format is slightly different_)
* Follow RESTful API web service architecture - _see ...RESTful md ..._
* Allows the rendering of other template with the current context {% includes "subfolder/another.html" %} 
(this should be move to the Django Template built-Ins features MD section: https://docs.djangoproject.com/en/3.0/ref/templates/builtins/)


Folder structure organized by `project` and `app`:
- Project = Website
- App = Website sections
- Template = Web pages on site
- Static = Supplementary js/css/images

## Create Django Project

   - activate vEnv before creating a Django project
   - create a project named `projName`
        ```python
        source veDjango/bin/activate
        django-admin startproject projName
        ```

## Create Django App

   - create an app named `appName` inside the project; test project run
        ```python
        python manage.py startapp appName
        python3 manage.py runserver
        ```

## Hook up project (settings.py)

- open OUTER/root level projName folder in VSCode
- activate vEnv
- arrive at outer level projName folder
- projName > settings.py > INSTALLED_APPS section
- add new app in list:
    ```python
    INSTALLED_APPS = [
        'appName’,
        'django.contrib.admin',
    ```


## Hook up project URLs (project/urls.py)

- locate urls.py in inner level projName folder
- import include clause
- point to app urls.py:
    ```python
    from django.urls import path, include
    urlpatterns = [
            path('', include('appName.urls')),
    ]
    ```

## Hook up app URLs (app/urls.py)
- locate/add urls.py in appName folder
- import view from same directory level
- point to views functions
    ```python
    from django.urls import path
    from . import views
    urlpatterns = [
        path('', views.indexPg),
        path(‘create’, views.create),
        path(‘<id>/<name>’, views.update),
    ]
    ```

## Hook up views and functions
- locate views.py in the same appName folder
- import render, HttpResponse and redirect
- create function using same name in views reference
    ```python
    from django.shortcuts import render, HttpResponse, redirect
    def indexPg(request):
        return HttpResponse("First Django Project Exercise!")
        return render(request, “index.html”)	

    def create(request):
        return redirect(“/“)      <= / redirects to main (root) URL

    def passData(request, name, id):
        context = {
                “name”: name,
                “favorite_color”: id,
                “pets”:[“Skittles”,”Vanilla”,”Apricot”]
        }
    return HttpResponse(f”name is {name} and fav_color is {favorite calor}”)	
    return render(request, “htmlFileToBeRendered.html”, context)
    ```
		
## Hook up HTML
- create a `templates` directory folder inside appName to house .html files
    
    @ htmlFileToBeRendered.html
    ```html
        <h1>Info From Server:</h1>
        <p>Name: {{name}}</p>
        <p>Color: {{favorite_color}}</p>
        <p>Pets</p>
        <ul>
        {% for pet in pets %}
        <li>{{pet}}</li>
        {% endfor %}
        </ul>
    ```
    ```django
        array[0] => {{ array.0 }}  use . in place of square brackets in Django Template
        {# 1 liner comment #}      1 liner comment in Django Template
        {% block                   block comment in Django Template
            … … 
        comment %}
    ```
    - Beware of TYPOs - case sensitive!!
    - REMEMBER: Response! Request!  NOT: resource!!!
    - test run server frequently!
	
## Hook up JavaScript/CSS scripts

- create a `static` folder holds js/css/image - static/css/style.css
    ```html
    <html>
        ...
        <title>IndexPg</title>
        {% load static %}
        <link rel="stylesheet" href="{% static 'css/style.css' %}">
        <body>
        <img src=“{% static ‘images/image.jpg’ %}” />
    ```









---
## Need help with PY command
```
python3 -help
```

## Hook up `python` to the latest python version
> This is for if you want to be able to type `python` instead of `python3` for all the commands because `python` give you an error 
- first check where it is installed: 
    ```python
    ls -l /usr/local/bin/python*
    ```
- should see something similar to this:
- only focus on `python3.#` - ignore the ones ending with `config` or `python3.*m` or `python3.*m-config`
    ```
    lrwxr-xr-x  1 root        wheel  69 Mar  1 10:43 /usr/local/bin/python3 -> ../../../Library/Frameworks/Python.framework/Versions/3.8/bin/python3
    lrwxr-xr-x  1 root        wheel  76 Mar  1 10:43 /usr/local/bin/python3-config -> ../../../Library/Frameworks/Python.framework/Versions/3.8/bin/python3-config
    lrwxr-xr-x  1 root        wheel  71 Mar  1 10:43 /usr/local/bin/python3.8 -> ../../../Library/Frameworks/Python.framework/Versions/3.8/bin/python3.8
    lrwxr-xr-x  1 root        wheel  78 Mar  1 10:43 /usr/local/bin/python3.8-config -> ../../../Library/Frameworks/Python.framework/Versions/3.8/bin/python3.8-config
    ```
- adjust and point `python` to the latest PY version:
- if the path to python does not exist, this command will create it
    ```python
    ln -s -f /usr/local/bin/python3.8  /usr/local/bin/python 
    ```
- restart Terminal; check python version now:
    ```
    python --version    or    python -V
    ```
- now you should be able to use PY commands with `python` without the trailing `3`