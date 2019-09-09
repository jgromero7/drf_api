# DRF-API

This is a django project entitled DRF-API. It has the basic configurations to start an api restful project and is pre configured for production deployment.
### Features

DRF-API uses a number of open source projects to work properly:

* [DJango](https://docs.djangoproject.com/en/2.2/) - Python web framework version 2.2.5
* [DJango Rest Framework](https://www.django-rest-framework.org/) - Django REST framework is a powerful and flexible toolkit for building Web APIs. Version 3.10.3
* [PyMySQL](https://pypi.org/project/PyMySQL/) - Python module for handling MySQL database, This package contains a pure-Python MySQL client library, based on PEP 249. Version 0.9.3
* [Python-Dotenv](https://pypi.org/project/python-dotenv/) - Reads the key,value pair from .env file and adds them to environment variable. It is great for managing app settings during development and in production
* [django-environ](https://pypi.org/project/django-environ/) - allows you to use Twelve-factor methodology to configure your Django application with environment variables. Version 0.4.5
* [Gunicorn](https://pypi.org/project/gunicorn/) - ‘Green Unicorn’ is a Python WSGI HTTP Server for UNIX. It’s a pre-fork worker model ported from Ruby’s Unicorn project. Version 19.9.0

And of course DRF-API itself is open source with a [public repository](https://github.com/jgromero7/drf_api)
 on GitHub.

### Installation

DRF-API requires [Python](https://www.python.org/downloads/) v3.6.+,  [virtualenv](https://virtualenv.pypa.io/en/latest/) v16.7.+ and [pip3](https://pip.pypa.io/en/stable/) to run.

```bash
$ virtualenv venv
$ source venv/bin/activate
# You may want to change the name `drf_api`.
$ django-admin startproject \ 
    --template https://github.com/jgromero7/drf_api.git drf_api
```
#### Install the dependencies.

```sh
$ cd drf_api
$ pip install -r requirements.txt
```

#### Environment variables
These are common between environments. The `ENVIRONMENT` variable loads the correct settings, possible values are: `DEVELOPMENT`, `STAGING`, `PRODUCTION`.

```sh
ENVIRONMENT='DEVELOPMENT'
DEBUG=True
SECRET_KEY='k1#rlh7+(8dx_$bz9fx@m$$4+nzvc+frd$zb2gia#b$8pr67%i'
# Add comma separated host, exapmle: 'diminio.com,www.dominio.com'
# To allow all access not to add values
ALLOWED_HOSTS=''
```
Language, time zone and location settings 
```sh
LANGUAGE_CODE = 'en-us'
TIME_ZONE='UTC'
USE_I18N=True
USE_L10N=True
USE_TZ=True
```
These settings(and their default values) are only used on staging and production environments.
```sh
DB_ENGINE='mysql'
DB_NAME=''
DB_USER=''
DB_PASSWORD=''
DB_HOST=''
DB_PORT=''
```

#### Run migrations
```sh
$ python manage.py migrate
```

### Run Project Development
```sh
$ python manage.py runserver
```

Verify the deployment by navigating to your server address in your preferred browser.

```sh
127.0.0.1:8000 || http://localhost:8000
```

### Solve mysqlclient error
```sh
Refer error: django.core.exceptions.ImproperlyConfigured: mysqlclient 1.3.13 or newer is required; you have 0.9.3.
```
Edit File base.py and commented `raise ImproperlyConfigured`
```sh
$ cd ../venv/lib/python3.6/site-packages/django/db/backends/mysql/base.py
```
```python
if version < (1, 3, 13): 
    pass
    # raise ImproperlyConfigured('mysqlclient 1.3.13 or newer is required; you have %s.' % Database.__version__)
```

Edit File operations.py and replace `query.decode` with `query.encode`
```sh
$ cd ../venv/lib/python3.6/site-packages/django/db/backends/mysql/operations.py
```
```python
    # query = query.decode(errors='replace')
    query = query.encode(errors='replace')
```

Repeat the process again:: `Run Project Development`

### Development
It is possible to deploy to `nginx` and  `gunircorn` in to your own server.

License
----

MIT

Autor: José Romero
----

**Free Software, Hell Yeah!**

