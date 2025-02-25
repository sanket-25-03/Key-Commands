### **1. Sample DRF ViewSet & Model**
Let's assume you have a `Book` model and a `BookViewSet`:

#### **models.py**
```python
from django.db import models

class Book(models.Model):
    title = models.CharField(max_length=255)
    author = models.CharField(max_length=255)
    published_date = models.DateField()
```

#### **serializers.py**
```python
from rest_framework import serializers
from .models import Book

class BookSerializer(serializers.ModelSerializer):
    class Meta:
        model = Book
        fields = "__all__"
```

#### **views.py**
```python
from rest_framework import viewsets
from .models import Book
from .serializers import BookSerializer

class BookViewSet(viewsets.ModelViewSet):
    queryset = Book.objects.all()
    serializer_class = BookSerializer
```

#### **urls.py**
```python
from django.urls import path, include
from rest_framework.routers import DefaultRouter
from .views import BookViewSet

router = DefaultRouter()
router.register(r'books', BookViewSet)

urlpatterns = [
    path('api/', include(router.urls)),
]
```

---

### **2. Pytest Tests for CRUD Operations**
Now, let's write tests for the `BookViewSet` API.

#### **tests/test_book_api.py**
```python
import pytest
from rest_framework.test import APIClient
from django.contrib.auth.models import User
from .models import Book

@pytest.fixture
def api_client():
    return APIClient()

@pytest.fixture
def create_user(db):
    return User.objects.create_user(username="testuser", password="testpass")

@pytest.fixture
def auth_client(api_client, create_user):
    api_client.force_authenticate(user=create_user)
    return api_client

@pytest.fixture
def create_book(db):
    return Book.objects.create(title="Django for Beginners", author="William S. Vincent", published_date="2021-05-10")

def test_create_book(auth_client):
    data = {
        "title": "Python Crash Course",
        "author": "Eric Matthes",
        "published_date": "2019-04-21"
    }
    response = auth_client.post("/api/books/", data, format="json")
    assert response.status_code == 201
    assert response.data["title"] == "Python Crash Course"

def test_list_books(auth_client, create_book):
    response = auth_client.get("/api/books/")
    assert response.status_code == 200
    assert len(response.data) == 1
    assert response.data[0]["title"] == "Django for Beginners"

def test_get_single_book(auth_client, create_book):
    response = auth_client.get(f"/api/books/{create_book.id}/")
    assert response.status_code == 200
    assert response.data["title"] == "Django for Beginners"

def test_update_book(auth_client, create_book):
    data = {"title": "Django Advanced", "author": "William S. Vincent", "published_date": "2021-05-10"}
    response = auth_client.put(f"/api/books/{create_book.id}/", data, format="json")
    assert response.status_code == 200
    assert response.data["title"] == "Django Advanced"

def test_delete_book(auth_client, create_book):
    response = auth_client.delete(f"/api/books/{create_book.id}/")
    assert response.status_code == 204
    assert Book.objects.count() == 0
```

---

### **3. Running the Tests**
Run tests using:
```bash
pytest -v
```s
