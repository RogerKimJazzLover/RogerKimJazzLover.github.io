---
layout: single
title: "django: intro to DRF"
categories: django
tag: [django, back-end, python, rest-api, drf]
---
## Introduction
This post explains the basic features of django DRF's serializer.

### Serializer?
- Serializer is a handy tool / component built in the Django Rest Framework, that helps you **convert complex data** such as querysets and model instances **into python datatypes** that can then be turned into JSON or other content types. It **also allows** you to convert the **parsed data back into complex types**, after validating the data

## Getting Started

### Why do we need it?
Suppose that you have a UserProfile model looking like this
```python
class UserProfile(models.Model):
    uid = models.UUIDField(primary_key=True, default=uuid.uuid4, 
                           editable=False, unique=True)
    user = models.ForeignKey(User, on_delete=models.CASCADE, 
                             related_name='profiles')
    profile_pic = models.ImageField(null=True)

    profile_name = models.CharField(null=True, max_length=30)

    bio_title = models.CharField(null=True, max_length=40)
    bio = models.CharField(null=True, max_length=155)
    
    job_title = models.CharField(null=True, max_length=40)
    job_description = models.CharField(null=True, max_length=155)

    # and perhaps some more fields

    def __str__(self):
        return f'{self.user.email} - Profile'
```
Now imagine creating an instance of that in views.py using the data from the request. It would look something like this
```python
# !! ASSUMING YOU ALREADY HAVE A 'user' object
post_data = request.data
try:
    profile_name = post_data['profile_name']
    bio_title = post_data['bio_title']
    bio = post_data['bio']
    job_title = post_data['job_title']
    job_description = post_data['job_description']
except KeyError:
    # handling error in case the post data doesn't contain certain values

# manually creating an instance
instance = UserProfile.create(user=user, email = email, 
                            profile_name = profile_name 
                            ...
                            )
```
This already looks repetitive, and an error can easily occur. **This is NOT what we want**. Which is exactlly what serializers are for.

With serializer, the code would looke like this. The serializer would help convert the python's datatypes into a complex model instance.
```python
# with serializer
instance = UserProfileSerializer(data=request.data)
if instance.is_valid():
    instance.save(user=user)
```

## Setting Up
1. Create a `serializers.py` file
2. Creating a serializer component
    ```python
    # import the necessary modules
    from rest_framework import serializers
    from .models import UserProfile

    class UserProfileSerializer(serializers.ModelSerializer):
        # you can set read only fields as well
        uid = serializers.UUIDField(read_only=True)
        name = serializers.SerializerMethodField(read_only=True)
        gender = serializers.SerializerMethodField(read_only=True)
        age = serializers.SerializerMethodField(read_only=True)

        # defining the fields that the serializer is going to include
        class Meta:
            model = UserProfile
            depth = 1
            fields = [   
                "uid", 
                "profile_name", 
                "bio_title",
                "bio", 
                "job_title",
                "job_description",
                
                # You can even get data from the User instance that
                # the serializer is linked to
                "name",
                "gender",
                "age", 
            ]

        def get_name(self, obj):
            return obj.user.name
        def get_age(self, obj):
            return obj.user.age
        def get_gender(self, obj):
            return obj.user.gender
    ```
    `depth`
    - _The depth option should be set to an integer value that **indicates the depth of relationships** that should be traversed before reverting to a flat representation_(from official doc)
    
    `fields`
    - a list of strings that indicates which fields is included in this serializer

    the `get_{field name}` functions
    - some data's cannot be directly queried, or you may want to customize the values of some fields.
    - that is when you use the functions starting with `get`. So for example, the `get_name` function in the code above reads the `name` field from the user instance that is set as foreign key to the UserProfile model, and allow us to easily access it just via serialzer

## How to use
### Python Datatype -> Complex Data
### Complex Data -> Python Datatype


## Contact Me:
Roger Kim

[Github](https://github.com/RogerKimJazzLover)

e-mail: <minseungkim1017@gmail.com> 