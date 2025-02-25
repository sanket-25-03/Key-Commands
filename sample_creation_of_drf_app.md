### 1. **Set Up a Virtual Environment**
```bash
python -m venv venv
source venv/bin/activate  # On Windows use: venv\Scripts\activate
```

---

### 2. **Install Django and Django REST Framework**
```bash
pip install django djangorestframework
```

---

### 3. **Create a Django Project**
```bash
django-admin startproject myproject
cd myproject
```

---

### 4. **Create a Django App**
```bash
python manage.py startapp myapp
```

---

### 5. **Register the App and DRF in `settings.py`**
Edit `myproject/settings.py`:
```python
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',

    'rest_framework',  # Add DRF
    'myapp',  # Add your app
]
```
