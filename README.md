# markdown
# Outline for Ontario Covid-19 App

## Develop backend using Django

### Create a virtual environment
```
	python -m venv env # If python was not installed.
	cd env/scripts
	activate
```
### Create Django project
```
	pip install django
	django-admin startproject django_project
```
### Create Django app
```
	cd myapp
	python manage.py startapp covid_ON
```
```
	INSTALLED_APPS = [
	    …
	    Covid_ON,
	]
```
```
	python manage.py makemigrations
	python manage.py migrate
```

### Create boundary map file

Create a folder data at the same level of covid_ON

```
	django_project/
	├── data/
	├── django_project/
	│   ├── __init__.py
	│   ├── asgi.py
	│   ├── settings.py
	│   ├── urls.py
	│   └── wsgi.py
	├── covid_ON/
	│   │
	│   ├── migrations/
	│   │   └── __init__.py
	│   │
	│   ├── __init__.py
	│   ├── admin.py
	│   ├── apps.py
	│   ├── models.py
	│   ├── tests.py
	│   └── views.py
	└── manage.py

```

Download geojson file (_Ministry\_of\_Health\_Public\_Health\_Unit\_Boundary.geojson_) from [https://geohub.lio.gov.on.ca/datasets/ministry-of-health-public-health-unit-boundary/explore?location=48.675153%2C-84.749434%2C5.73](https://geohub.lio.gov.on.ca/datasets/ministry-of-health-public-health-unit-boundary/explore?location=48.675153%2C-84.749434%2C5.73) by clicking cloud download in view full detail, and then download in the geojson option

Locate the file to the data folder,

Rename the file to phu\_Ontario.json

### Setting up API

```
	pip install Django-Rest-Framework
	pip install django-cors-headers
	pip install django-rest-auth
```

Add rest_auth, rest_framework.authtoken, rest_framework, corsheaders rest_auth app to INSTALLED\_APPS in your django settings.py

```
	INSTALLED_APPS = [
		…
		'corsheaders',
		'rest_framework',
		'rest_framework.authtoken',
		'rest_auth',
	]

```

Add a middleware class to django settings.py

```
	MIDDLEWARE = [
		…	
		'django.middleware.security.SecurityMiddleware',
		'corsheaders.middleware.CorsMiddleware',
		'django.middleware.common.CommonMiddleware',
		…,
	]

```


Read the file and store it into base\_map variable using code

```
	import json
	from pathlib import Path
	import os

	ROOT_DIR = Path(__file__).parent.parent
		path = os.path.join(ROOT_DIR, "data", "phu_ON.json")
		with open(path) as f:
			base_map = json.load(f)

```
