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
To do that we can type python3 manage.py startapp todo
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


