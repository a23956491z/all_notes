---
tags : web-develop python
---

## 安裝環境

虛擬環境
```bash
$ pip3 install virtualenvwrapper-win
$ mkvirtualenv my_django_environment
```

虛擬環境常用命令：
* `deactive` 退出當前[[Python]]虛擬環境
* `workon` 列出可用環境
* `wokron environment` 啟動指定Python虛擬環境
* `rmvirutalenv environment` 刪除指定環境

安裝Django
`$ pip3 install django`
測試安裝
```bash
$ mkdir django_test
$ cd django_test
$ django-admin startproject mytestsite
$ cd mytestsite
```
瀏覽 http://127.0.0.1:8000/

## Server Skeleton

**Create project**
```bash
$ mkdir django_projects
$ cd django_projects
$ django-admin startproject locallibrary
$ cd locallibrary
```

**Struct intro**
```
locallibrary/
    manage.py
    locallibrary/
        __init__.py
        settings.py
        urls.py
        wsgi.py
        asgi.py
```
* **__init__.py** is empty file that instructs Python treat this directory as Python package.
* **settings.py**
* **urls.py** defines the site URL-to-view mappings.
* **wsgi.py** help Django app communicate with webserver 
* **asgi.py** Standard for *Python asynchronous web apps & servers* communicate with each other.

**Setting SQL server**:*(locallibrary/locallibrary/settings.py)*
```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'mydatabase',
        'USER': 'test',
        'PASSWORD': 'test',
        'HOST': 'localhost',
        'PORT': '3306',
    }
}
```

## Create the catalog application
`py manage.py startapp catalog`

**Register the appilication**
* adding it to `INSTALLED_APPS` in project settings
* *(locallibrary/locallibrary/settings.py)*
```python
INSTALLED_APPS = [
	...
	
    'catalog',
]
```

**Hooking up the URL mapper**
* *(locallibrary/locallibrary/urls.py)*
```python
...

# Use include() to add paths from the catalog application 
from django.urls import include

urlpatterns += [
    path('catalog/', include('catalog.urls')),
]
```

Redirecting the root URL of our site (i.e. 127.0.0.1:8000) to the URL 127.0.0.1:8000/catalog/.
```python
#Add URL maps to redirect the base URL to our application
from django.views.generic import RedirectView
urlpatterns += [
    path('', RedirectView.as_view(url='catalog/', permanent=True)),
]
```

> Django does not serve static files like CSS, JavaScript, and images by default, but it can be useful for the development web server to do so while you're creating your site. As a final addition to this URL mapper, you can enable the serving of static files during development by appending the following lines. 
```python
# Use static() to add url mapping to serve static files during development (only)
from django.conf import settings
from django.conf.urls.static import static

urlpatterns += static(settings.STATIC_URL, document_root=settings.STATIC_ROOT)
```

**Create urls.py in *catalog/***
```python
from django.urls import path
from . import views

urlpatterns = [

]
```

## Testing the website framwork