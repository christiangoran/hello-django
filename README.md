# Hello Django

## Install Django

To ensure that you get the a version of django that will work while following these videos, instead of the command pip3 install django, please use this:

pip3 install 'django<4'

Django 3.2 is the LTS (Long Term Support) version of Django and is therefore preferable to use over the newest Django 4

## Hiding environment variables

Use the env.py file, and make sure this is added to .gitignore.

DO NOT put settings.py in .gitignore in an effort to hide the hardcoded SECRET_KEY.

## Starting Django Project

Django comes with the built-in admin command for things like starting projects
and other core functionality.
So let's use that to create a project.
We'll type

- django-admin startproject django_todo .

And put a dot at the end of this command this will signify that we want to create
this project in the current directory.
After this is written the folder "django_todo" is created as well as the "manage.py"-file.

The django_todo folder.
And manage.py is a management utility we'll need throughout the project.
If we open the django_todo folder there's an **init**.py file which was automatically
created to tell our project that this is a directory we can import from.

We've also got three key files in here.
**settings.py, urls.py and wsgi.py**
**settings.py** contains the global settings for our entire Django project. So things like whether we want to show debug information when errors happen.
And things like where our HTML templates are located. And which database we're going to connect to.
These are all controlled in the settings.py file

**urls.py** contains the routing information that allows our users to type a specific
URL into their address bar. And hit a specific Python function. So this is analogous to app.root in flask.

And finally we have **wsgi.py** which contains the code that allows our web server to communicate with our Python application.
And that's it. That's all we need to start a new Django project.

In order to run our project. We can use that manage.py utility.
By typing

python3 manage.py runserver

This will tell us that a service is listening on port 8000 but it's not exposed.
So we can expose that. And then click on open browser.

- ERROR: I got an error that was related to ALLOWED_HOSTS in the settings.py file.
    - It was sorted by adding "8000-christiangoran-hello-dja-y9ccm7u1e0.us2.codeanyapp.com" to ALLOWED_HOSTS = []

## Environment Variables
There are several efficient and flexible methods to deal with environment variables in Django, amongst them
using python-dotenv and django-environ
While both achieve the same, I recommend python-dotenv because it's a better maintained project with
regular updates, and so I will only focus on it.

**How to set up**
Install the package with your preferred package manager (pip, pipenv, poetry)

pip install python-dotenv 

Create a .env file at the same level as settings.py
Add your variables in that file as needed, with this format (no quotes required):

SECRET_KEY=yoursecretkey 
DEVELOPMENT=development 
ANY_OTHER_VARIABLE=anyothervalue 
Add the following to the top of your settings.py

# settings.py
from dotenv import load_dotenv 
load_dotenv() 
Call your variables either with os.getenv() or os.environ.get()
# settings.py
import os 
SECRET_KEY = os.environ.get("SECRET_KEY") 
DEBUG = "DEVELOPMENT" in os.environ 
Note that DEBUG will be True if there's a DEVELOPMENT key/value pair in your .env file, regardless of
its value (i.e. if it has any value it will be True).
This means that DEBUG will be False in production, unless the DEVELOPMENT variable is added to the
production host's environment variables.
Don't forget to add .env to your .gitignore and never track it with version control