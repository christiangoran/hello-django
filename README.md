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

- django-admin startproject django_todo . (do not forget the dot in the end, to install in root directory)

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

db.sqlite3.
This file will act as our database for the project. Quite important.

## URLs

There is a couple of items were automatically generated.
The pycache directory which contains compiled python code.
And the more important one here which is db.sqlite3.
This file will act as our database for the project.
So you want to be really careful not to delete or change this file in any way.
Since doing so will cause a lot of problems with our project.
And most likely make any data that we've put into the database unrecoverable.
With that said let's talk a bit more about how Django works.
Django projects are organized into small components called apps.
You can think of an app as a reusable self-contained collection of code.
That can be passed around from project to project in order to speed up development time.
So if you need an authentication system for example that handles logging in
logging out password resets and so on.
Rather than build your own you could use a Django app. And simply install it into your project.
Almost everything that we do in Django is going to revolve around these apps.

So let's create one now using the manage.py startapp command.
Since we're going to build a to-do list. Let's create an app called todo
To do that we can type:

- python3 manage.py startapp todo

You'll see this creates another folder called todo in the file explorer.
And if we open that folder we'll see a number of other items
We'll get to all of these eventually but for now we're going to focus on
only one of them and that file is views.pi
If we want to build a todo list web application.
The first thing that we obviously need to be able to do is render some sort of
web page
You might recall from the intro video to this module that the views in the model
view template design pattern.
Are the mechanism by which users on the front end of our app can communicate
with the back end where the data lives.
In our case, that data is going to be our to-do items.
So we need to render some sort of an interface that allows our users to interact with those items
Just to demonstrate how this is going to work.
Let's define a simple python function in views.py called say_hello
And literally all this python function is going to do.
Is take an http request from the user and return an http response
to the user that says hello
And that's it. We're gonna need to import HttpResponse from the Django shortcuts
which is built into Django.
So we're going to import that here. And we'll talk more about this later.
But for now just go ahead and import it. And that's it.
So our python function is done.
And it should say hello.
**But how do we make this function available to the web browser.**
**The answer is we do it through urls.py which we spoke about briefly in the last video.**
In order to bring the pieces together here let's go to urls.py. And before we do anything else
We know that we're going to need our python function from the views file.
So let's import that right here at the top. By typing from todo.views import say_hello
This is going to allow us to use the say_hello function inside of the urls file.
Once that's done all that we need to do is define the url that's actually going to
trigger the say hello function and return the http response to the browser.
To do that we use the built-in path function which typically takes three arguments.
It takes the url that the user is going to type in. In our case we're going to say hello.
It takes the view function that it's going to return.
Which is our say_hello function.
And it takes a name parameter which we'll get to a bit later but for right now we'll just call it hello
And that's it that's all it takes. So if we go ahead and save this file now.
Jump down to our terminal and type python3 manage.py runserver
to start our Django application.
We'll see we have the service running now. And we get a service available on port 8000
We can open the browser.
And we get page not found why. Because we haven't typed /hello
At the end of the url
And there we go. There's our hello function saying hello to the browser.
End of transcript. Skip to the start.

## Migrations

We keep getting this warning that we've got unapplied migrations and that our project may not work properly until we apply them.
The warning tells us that we can run this migrate command from the manage.py

Migrations are Django's way of converting Python code into database operations. In other words when you need to make changes to a database connected to a Django project.Instead of running raw sequel commands or using some other database language. Django will do everything for you and all you need to do is write Python code.
The reason that we keep getting that warning when we run our project is because Django recognizes that even though we've created a new project and started an app.
We haven't actually done anything to set up the sequel lite database that it created for us it's telling us that we need to run all the initial built-in database operations.

- python3 manage.py makemigrations (--dry-run can be used to simulate a command)

  - This one needs to be done when models are added that we want in our database. The command tells Django to convert the Python code to SQL Code.

- python3 manage.py showmigrations.

  - There are some built-in Django apps like authentication and the Django admin and a couple of others that already have some migrations that need to be applied. And applying these migrations we'll set up the database and allow us to create an admin user that we can use to manage it.

- python3 manage.py migrate (can be run with --plan can be written to make the terminal show what it will do first)

  - These initial migrations are going to take care of some basic requirements like setting up the users groups and permissions tables and altering the fields on some of those tables.

- python3 manage.py createsuperuser

  - This will create an admin and we will have to create a username, password and give an email (optional) To login to this add /admin to the url, and login to the admin account.

  ## Models

  Under the Django app folder todo we fint the file models.py - This is the file used to create database models.

  Here is an example of how a model can look like. "models.Model" And here's a key thing to understand here though. And that's that by itself this class won't do anything. We need to use something called class inheritance to give it some functionality. And by using "models.Model" we inherit the functionality from a model that Django has created for us.

  class Item(models.Model):
  name = models.CharField(max_length=50, null=False, blank=False)
  done = models.BooleanField(null=False, blank=False, )

After the model is created we need to run

- python3 manage.py makemigrations.

For Django to create SQL code out of the python code, and puts into a .py file under todo/migrations folder.

We can also use the

- python3 manage.py showmigrations

command to see that we do in fact have an unapplied migration on our to-do app now. And to apply it all we need to do is run

- python3 manage.py migrate

Even though the items table has been created and we could start creating items programmatically now.
We won't be able to see our items in the admin until we expose them. To do that we need to register our model in the todo apps admin.py file.
In admin.py we can import our item model from .models

In the admin.py file we write

- from .models import Item (that is the name of our class model)

Then below to actually register our Item model I write:

- admin.site.register(Item) Item is the name of the class we want to register

And to actually see the name of the item created in the todo list. We also need to redefine the generic object name by adding the following to **models.py**

def **str**(self):
return self.name

So this is going to return the item class's name attribute and display it on the webpage.

## Rendering the data

So to show our display our models to the user we need to get back to the views.py template that represents the programming logic that users can interact with the database through the template that they see.

First thing to do in the views.py is to add

- from .models import Item (or whatever other name of the model that we want to use)

Then in our (in this case) get_todo_list function in views.py we can get what's called a query set of all the items in the database.

- items = item.objects.all

Next I'm going to create a variable called context. Which is just going to be a dictionary with all of our items in it.

- context = {
  'items' : items
  }

And finally I'm going to add that context as a third argument to the render function. And this will ensure that we have access to it in our todo list .html template.

After this I add a template variable with the items name into the .html-file I want it displayed in {{ items }}
template variables can show almost anything that you can use in Python Meaning you can return strings, numbers, lists, other dictionaries, or even functions and classes.
