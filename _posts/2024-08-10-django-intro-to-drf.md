---
layout: single
title: "django: intro to DRF"
categories: django
tag: [django, back-end, python, rest-api, drf]
---
## Introduction
In this post, I am going to talk about
- how to set up Django Rest Framework(DRF) in Debian/Ubuntu
- basic features of DRF
- class-based views

## Setting up DRF
**Frist,** let's install the necessary dependencies. There are two options, one with `pip`, and other with `poetry` which I introduced in [this post](https://rogerkimjazzlover.github.io/python/python-dependency-management-with-poetry/)

- `pip install djangorestframework` or `poetry add djangorestframework`

**Second,** add `rest_framework` to `INSTALLED_APPS` array in your _settings.py_ file.
```python
# settings.py
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    '<your_other_apps>',

    # add this
    'rest_framework',
]
```
**Third,** set up your app like you would set up any other django apps! (create urls.py, register it to the root/main urls.py, etc.)

**Lastly,** include the necessary dependecies to your views.py and you are **good to go!**
```python
# views.py
from rest_framework.decorators import api_view
from rest_framework.response import Response
from rest_framework import status 

# some other modules that are useful
from rest_framework.request import Request # for hinting
```

## Basic DRF Features
The most bascic feature of DRF is functional views with the `api_view` decorator. DRF, as the name suggests, is used to build REST APIs with django. 
- For action based APIs, functional views are often used. 
- For object-based APIs, ***classed-based views*** are used, which will be discussed in the next section.
```python
@api_view(['GET'])
def health(request):
    return Response({"status":"All Good"}, status=status.HTTP_200_OK) 
```
This code shows some of the basic features of DRF. The `api_view` decorator, the `Response` module and the `status` module.
- `api_view` decorator
    - This decorator indicates what types of http methods the function can handle. In this example, it can handle `GET` request only. But as you can see, it is a **list**. So you can put multiple methods there.
- `Response` and `status` module
    - This creates an response object to be returned. You can indicate the status of your resposne using `status=status.HTTP_blah_blah`.

With these three simple modules, you can already build a fully functioning REST API, if you integrate django's ORM into the functions. ***However,*** REST APIs are often times ***object-based.***

## Class-Based Views

### Object-based?
Here are some example of url endpoints for REST APIs.
- `/api/users?email=asdf@asdf.com`
- `/api/products/123456`

If you change around the http method between `POST`, `GET`, `PUT`, `DELETE`,
it basically becomes a ***CRUD [Create(POST), Read(GET), Update(PUT), Delete] operations*** to certain ***objects.*** Which is where ***class-based views** comes in handy.

On top of that, in order fully integrate class-based views, you msut know ***serializers***. Which I will discuss in a seperate post due to its length. But you can always search up tutorials yourself. Here's a great tutorial I found.
- _CodingEntrepremeurs._ _Build a Django REST API with the Django Rest Framework. Complete Tutorial._
    
    https://www.youtube.com/watch?v=c708Nf0cHrs&list=PL0yqfPf4QbKGmyi-8DG1GVoESHs9tiY3z&index=67

So in this post, I am only going to expalin the elements of class-based views and not serializers. 

### Here's a **dumy-code** that well-displays how class-based views can be used for CRUD operations.

```python
# additional module
from rest_framework import generics

# importing models and serializers
from your_app.serializers import UserSerialzier
from your_app.models import User

class UserView(generics.CreateAPIView, generics.RetrieveAPIView):
    '''
    Class for creating, reading, updating and deleting users
    '''
    queryset = User.objects.all()
    serializer_class = UserSerializer
    # permission_classes = [IsAuthenticated]

    def post(self, requests):
        try:
            user = User.objects.create_user(
                email=request.data['email'],
            )
        except Exception as e:
            return Response({"error":"Invalid Fields","exception":f"{e}"}, 
                            status=status.HTTP_400_BAD_REQUEST)

        return Response({"message":"User created successfully"},
                            status=status.HTTP_201_CREATED) 
    
    def put(self, request):
        user = User.objects.get(email=request.data['email'])
        serializer = self.get_serializer(user, data=request.data)
        if serializer.is_valid():
            serializer.update(instance=user, validated_data=request.data)
            return Response({"message":"User data updated successfully"}, 
                            status=status.HTTP_200_OK)
        return Response({"error":serializer.error_messages}, 
                            status=status.HTTP_400_BAD_REQUEST)
        
    def get(self, request):
        email = request.query_params.get('email')
        user = User.objects.get(email=email)
        serializer = self.get_serializer(user)
        return Response(serializer.data)
    
    def delete(self, request):
        user = User.objects.get(email=request.data['email'])
        user.delete()
        return Response({"message":"User deleted successfully"}, 
                            status=status.HTTP_204_NO_CONTENT)
```
Then in urls.py,
```python
# urls.py
from django.urls import path
from . import views

urlpatterns = [
    path("users/", views.UserView.as_view()),
    ...
]
```
- This piece of dummy code show how you can use class-based views to perform CRUD on a certian ***queryset*** using different http methods.
- So **the function names matters.** `get` function would handle `get` requests, and so on. But you can also always add you own functions into the class with a different name, that you can use for other purposes than handling user requests.
- `generics.CreateAPIView` and `generics.RetrieveAPIView`
    - https://www.django-rest-framework.org/api-guide/generic-views/#concrete-view-classes
    - there are different types of `generic` views that allow the class-based view to perform different actions. For basic CRUD, those two views would work. You can always refer to the official documentation above for more info.
- `permission_classes`
    - The code was commented out because the this post doesn't talk about **authenticating** users.
    - But if yuo have your authentication methods set up, you can set the permissions classes accordingly. Here's the offical documentation for it.
    - https://www.django-rest-framework.org/api-guide/permissions/#api-reference
- `serializer_class`
    - This instance defines which serializer you are going to user in the class.
    - In the code, the `self.get_serializer` function was able to be used due to the instance.
- Other codes are basically querying from the queryset using django's **ORM** and **serializer**
- **I will talk about serializers in a seperate post.**

## Contact Me:
Roger Kim

[Github](https://github.com/RogerKimJazzLover)

e-mail: <minseungkim1017@gmail.com> 