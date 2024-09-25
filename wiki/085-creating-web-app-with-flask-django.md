## 85. How do you create a web application using `Flask` or `Django`?


Creating a web application using `Flask` or `Django` involves different approaches, as these frameworks cater to different needs. `Flask` is a lightweight, micro web framework, while `Django` is a full-fledged web framework that comes with many built-in features. Below are step-by-step guides for building a simple web application using both `Flask` and `Django`.

### 1. **Creating a Web Application with `Flask`**

`Flask` is ideal for small to medium-sized applications where you need flexibility and control over your components.

#### **Step 1: Install Flask**

First, you need to install `Flask`:

```bash
pip install flask
```

#### **Step 2: Create a Basic Flask Application**

Create a new directory for your project and navigate into it:

```bash
mkdir flask_app
cd flask_app
```

Create a Python file named `app.py`:

```python
from flask import Flask, render_template

app = Flask(__name__)

@app.route('/')
def home():
    return render_template('index.html')

@app.route('/about')
def about():
    return "This is the About page."

if __name__ == '__main__':
    app.run(debug=True)
```

- **Explanation:**
  - `Flask(__name__)`: Creates a Flask application instance.
  - `@app.route('/')`: Defines the route for the home page (`/`).
  - `render_template('index.html')`: Renders the `index.html` template.
  - `app.run(debug=True)`: Runs the application with debugging enabled.

#### **Step 3: Create Templates**

Create a folder named `templates` in the project directory and add an `index.html` file:

```
flask_app/
    ├── app.py
    └── templates/
        └── index.html
```

`index.html`:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Flask App</title>
</head>
<body>
    <h1>Welcome to the Flask App</h1>
    <p>This is the home page.</p>
</body>
</html>
```

#### **Step 4: Run the Application**

Run your Flask application:

```bash
python app.py
```

Navigate to `http://127.0.0.1:5000/` in your web browser to see the application.

### 2. **Creating a Web Application with `Django`**

`Django` is suited for larger applications that require built-in features like authentication, admin interface, ORM, and more.

#### **Step 1: Install Django**

First, install `Django`:

```bash
pip install django
```

#### **Step 2: Create a Django Project**

Create a new Django project using the following command:

```bash
django-admin startproject myproject
cd myproject
```

This will create the following structure:

```
myproject/
    ├── manage.py
    ├── myproject/
    │   ├── __init__.py
    │   ├── asgi.py
    │   ├── settings.py
    │   ├── urls.py
    │   └── wsgi.py
```

#### **Step 3: Create a Django App**

Within the project, create a new app:

```bash
python manage.py startapp myapp
```

Add the app to the `INSTALLED_APPS` in `myproject/settings.py`:

```python
INSTALLED_APPS = [
    # Default apps
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',

    # Your app
    'myapp',
]
```

#### **Step 4: Define Views**

Edit `myapp/views.py` to create views:

```python
from django.http import HttpResponse
from django.shortcuts import render

def home(request):
    return render(request, 'index.html')

def about(request):
    return HttpResponse("This is the About page.")
```

#### **Step 5: Configure URLs**

Edit `myproject/urls.py` to include your app’s URLs:

```python
from django.contrib import admin
from django.urls import path
from myapp import views

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', views.home, name='home'),
    path('about/', views.about, name='about'),
]
```

#### **Step 6: Create Templates**

Create a `templates` directory inside your app and add `index.html`:

```
myproject/
    ├── manage.py
    ├── myproject/
    │   ├── settings.py
    │   ├── urls.py
    └── myapp/
        ├── views.py
        └── templates/
            └── index.html
```

`index.html`:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Django App</title>
</head>
<body>
    <h1>Welcome to the Django App</h1>
    <p>This is the home page.</p>
</body>
</html>
```

#### **Step 7: Run the Application**

Run the development server:

```bash
python manage.py runserver
```

Navigate to `http://127.0.0.1:8000/` in your web browser to see the application.

### Summary

- **Flask:**
  - **Best for:** Small to medium-sized projects where you need flexibility and minimal overhead.
  - **Advantages:** Simple, lightweight, easy to learn, highly customizable.

- **Django:**
  - **Best for:** Large-scale projects with built-in features like authentication, ORM, admin interface, and more.
  - **Advantages:** Batteries-included, scalable, follows the "DRY" (Don't Repeat Yourself) principle, robust security features.

Both `Flask` and `Django` are powerful frameworks that cater to different needs. Choose `Flask` if you want simplicity and control, and choose `Django` if you need a comprehensive solution for complex applications.