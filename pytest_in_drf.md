## **1. Install Dependencies**
If you haven't installed `pytest` and related plugins, install them:

```bash
pip install pytest pytest-django djangorestframework
```

---

## **2. Configure pytest for Django**
Create a `pytest.ini` file in your project's root directory:

```ini
[pytest]
DJANGO_SETTINGS_MODULE = your_project.settings
python_files = tests.py test_*.py *_tests.py
```

Replace `your_project.settings` with your actual Django settings module.

---

## **3. Use `pytest` to Test DRF APIs**

### **Basic API Test Example**
Create a `tests/` directory inside your Django app (if not already there). Inside it, create a `test_views.py` file:

```python
import pytest
from rest_framework.test import APIClient
from django.contrib.auth.models import User

@pytest.fixture
def api_client():
    return APIClient()

@pytest.fixture
def create_user(db):
    return User.objects.create_user(username="testuser", password="testpass")

def test_user_login(api_client, create_user):
    response = api_client.post("/api/token/", {"username": "testuser", "password": "testpass"}, format="json")
    assert response.status_code == 200
    assert "access" in response.data
```

---

## **4. Run Tests**
Run `pytest` from your project root:

```bash
pytest
```
