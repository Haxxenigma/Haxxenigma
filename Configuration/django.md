# [Django](https://www.djangoproject.com/)

[==> (tutorial) <==](https://docs.djangoproject.com/en/4.2/intro/tutorial01/)

### [Install Python:](https://www.python.org/downloads/)

```shell
apt install python3
```

### [Install pip:](https://pip.pypa.io/en/stable/installation/)

```shell
python -m ensurepip --upgrade
```

### [Create a Virtual Environment:](https://docs.python.org/3/tutorial/venv.html)

```shell
pip install virtualenv
```

```shell
virtualenv venvname
```

- Linux/MacOS:

    ```shell
    source venvname/bin/activate
    ```

- Windows:

    ```shell
    venvname\Scripts\activate
    ```

### [Install Django:](https://www.djangoproject.com/download/)

```shell
pip install Django
```

<br>

## Start Project:

```shell
django-admin startproject projectname
```

```shell
cd projectname
```

### Start App:

```shell
python manage.py startapp appname
```

### appname/views.py:

```python
from django.http import HttpResponse


def index(request):
    return HttpResponse("Hello, world. You're at the appname index.")
```

### appname/urls.py:

```python
from django.urls import path
from . import views

urlpatterns = [
    path("", views.index, name="index"),
]
```

### projectname/urls.py:

```python
from django.contrib import admin
from django.urls import include, path

urlpatterns = [
    path("appname/", include("appname.urls")),
    path("admin/", admin.site.urls),
]
```

### Run Server:

```shell
python manage.py runserver
```

> Note that you must be at http://127.0.0.1:8000/appname/ and not http://127.0.0.1:8000/

> If you want http://127.0.0.1:8000/, then rewrite `projectname/urls.py's` 5th line to this: `path("", include("appname.urls"))`

## Working with Databases:

### appname/models.py:

```python
from django.db import models
from django.utils import timezone


class User(models.Model):
    username = models.CharField(max_length=50)
    password = models.CharField(max_length=100)
    date = models.DateTimeField(default=timezone.now)

    def __str__(self):
        return self.username
```

### projectname/settings.py:

```python
...
INSTALLED_APPS = [
    "appname.apps.AppnameConfig",
    "django.contrib.admin",
    "django.contrib.auth",
    "django.contrib.contenttypes",
    "django.contrib.sessions",
    "django.contrib.messages",
    "django.contrib.staticfiles",
]
...
...
LANGUAGE_CODE = "en-us"

TIME_ZONE = "Asia/Almaty"

USE_I18N = True

USE_TZ = True
...
```

### Make migrations:

```shell
python manage.py makemigrations
```

### Migrate:

```shell
python manage.py migrate
```

### Returns SQL of migrations:

```shell
python manage.py sqlmigrate appname 0001
```

### Invoke python shell:

```shell
python manage.py shell
```

- ### Import the model classes:

    ```python
    from appname.models import User
    ```

- ### Create data:

    ```python
    user = User(username="name", password="password")
    user.save()
    ```

- ### Read all data:

    ```python
    all_users = User.objects.all()
    ```

    ```python
    print(all_users[0].username)
    ```

    ```python
    for user in all_users:
        print(f"Username: {user.username}, Password: {user.password}")
    ```

- ### Filtered data:

    ```python
    filtered_users = User.objects.filter(username="name")
    ```

    ```python
    print(filtered_users[0].username)
    ```

    ```python
    for user in filtered_users:
        print(f"Username: {user.username}, Password: {user.password}")
    ```

- ### Single data:

    ```python
    single_user = User.objects.get(username="name")
    ```

    ```python
    print(single_user.username)
    ```

- ### Update data:

    ```python
    user = User.objects.get(username="name")
    user.username = "newname"
    user.save()
    ```

- ### Delete data:

    ```python
    user = User.objects.get(username="newname")
    user.delete()
    ```

- ### Using aggregations:

    ```python
    from django.db.models import Sum, Avg

    summary = User.objects.aggregate(Sum("fieldname"))
    average = User.objects.aggregate(Avg("fieldname"))
    ```

- ### Using annotations:

    ```python
    from django.db.models import F

    annotated_records = User.objects.annotate(new_field=F("fieldname1") + F("fieldname2"))
    ```

## Django Admin

```shell
python manage.py createsuperuser
```

### Login:

```
http://127.0.0.1:8000/admin/
```

### appname/admin.py:

```python
from django.contrib import admin
from .models import User

admin.site.register(User)
```

## Writing more views

### appname/views.py:

```python
from django.http import HttpResponse
from .models import User


def index(request):
    latest_users = User.objects.order_by("-date")[:5]
    output = ", ".join([u.username for u in latest_users])
    return HttpResponse(output)


def detail(request, user_id):
    response = "You're looking at user %s."
    return HttpResponse(response % user_id)
```

### appname/urls.py:

```python
from django.urls import path
from . import views

app_name = "appname"
urlpatterns = [
    path("", views.index, name="index"),
    path("<int:user_id>/", views.detail, name="detail"),
]
```

### Create "templates" directory:

```shell
mkdir ./appname/templates
mkdir ./appname/templates/appname
```

### appname/templates/appname/index.html:

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>

<body>
    <div class="main">
        {% if latest_users %}
        <ul>
            {% for user in latest_users %}
            <li><a href="{% url 'appname:detail' user.id %}">{{ user.username }}</a></li>
            {% endfor %}
        </ul>
        {% else %}
        <p>No users are available.</p>
        {% endif %}
    </div>
</body>

</html>
```

### appname/templates/appname/detail.html:

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>

<body>
    <div class="main">
        <h1>You're looking at user {{user}}</h1>
    </div>
</body>

</html>
```

### appname/views.py *(using templates)*:

```python
from django.http import HttpResponse
from django.http import Http404
from django.template import loader
from .models import User


def index(request):
    latest_users = User.objects.order_by("-date")[:5]
    template = loader.get_template("appname/index.html")
    context = {"latest_users": latest_users}
    return HttpResponse(template.render(context, request))


def detail(request, user_id):
    try:
        user = User.objects.get(pk=user_id)
        template = loader.get_template("appname/detail.html")
        context = {"user": user}
    except User.DoesNotExist:
        raise Http404("User does not exist")
    return HttpResponse(template.render(context, request))
```

### appname/views.py *(+using shortcuts)*:

```python
from django.shortcuts import render, get_object_or_404
from .models import User


def index(request):
    latest_users = User.objects.order_by("-date")[:5]
    context = {"latest_users": latest_users}
    return render(request, "appname/index.html", context)


def detail(request, user_id):
    user = get_object_or_404(User, pk=user_id)
    return render(request, "appname/detail.html", {"user": user})
```

## Use generic views

### appname/views.py:

```python
from django.views import generic
from .models import User


class IndexView(generic.ListView):
    template_name = "appname/index.html"
    context_object_name = "latest_users"

    def get_queryset(self):
        """Return the last five registered users."""
        return User.objects.order_by("-date")[:5]


class DetailView(generic.DetailView):
    model = User
    template_name = "appname/detail.html"
```

### appname/urls.py:

```python
from django.urls import path
from . import views

app_name = "appname"
urlpatterns = [
    path("", views.IndexView.as_view(), name="index"),
    path("<int:pk>/", views.DetailView.as_view(), name="detail"),
]
```

<br>

Final View of the [Django Project](./djangotest/projectname/)