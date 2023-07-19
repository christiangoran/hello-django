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

## Creating a new item

1. Duplicate todo_list.html and change header text
2. Add link to the page with href="/name_of_page"
3. Go to views.py, copy/create a new view variable

def add_item(request):
return render(request, "todo/add_item.html")

4. Go to urls.py and add a line under urlpatterns variable

path('add', add_item, name='add') <-- the first "add" is the name of the link, whatever_url/add in this case.

5. Also import the add_item from todo.views att the top of the urls.py page

6. Edit your html page
7. If a POST is required to a form or similar add

 <form method="POST" action="add">
        {% csrf_token %}

the csrf_token is required for it to work and is a random key that Django generates when creating the post, to verify
it is actually us that is making the post and not another site.

8. In case this is a POST item Finally we need to add this to the views.py:

def add_item(request):
if request.method == "POST": #Check that the request coming is from the button being pressed
name = request.POST.get('item_name')
done = 'done' in request.POST
Item.objects.create(name=name, done=done) #creates the new object

        return redirect('get_todo_list')

In this case this if statement recognizes if it is just a GET statement or a POST statement.

9. Import redirect from django.shortcuts at the top of views.py

## Using Django to create forms

1. First create a file called forms.py under the app-folder

2. add:
   from django import forms
   from .models import Item (or the name of the model class)

3. Then I add the following class:

class ItemForm(forms.ModelForm):
class Meta:
model = Item
fields = ['name', 'done']

This inner Meta class just gives our form some information about itself. Like which fields it should render how it should display error messages and so on.

4. Then we go to views.py and import the Itemform

- from .forms import ItemForm

5. Now we can create an instance of it in the add_item view

- form = ItemForm()
  context = {
  'form' : form
  }

And then return the context to the return render template

6. Now we can remove all the html code in the add_item.html and just put in a template variable

{{ form }}

7. Finally we need to add this to the views.py with:

def add_item(request):
if request.method == 'POST':
form = ItemForm(request.POST)
if form.is_valid():
form.save()
return redirect('get_todo_list')

## Edit existing items

1.  **Add HTML Link on main page** Add html code for edit buttons in the todo_list.html file with items IDs (easy misstake is to write items in plural instead if singular, goto first step in error searching)

            <td>
                <a href="/edit/{{ item.id }}">
                    <button>Edit</button>
                </a>
            </td>

2.  **Go to VIEW.py** Create a view in the view.py file

def edit_item(request, item_id):
return render(request, 'todo/edit_item.html')

3. **Create new app** Create a new app by duplicating/creating a new html file. I created edit_item.html

4. **Link it together in URLS.py** Update the urls.py, and do not forget to import the edit_item at the top of urls.py

path('edit/<item_id>', edit_item, name='edit')

5. **Go to VIEWS.py** Now we should be able to click the edit link and end up on the edit_item page. But we still have some things to do to actually retrieve the data to the page to be able to change it. So we need to retrieve the item data from the database.

under the variable edit_item() we add the following line, and id=item_id is what is passed into view from the url.

- item = get_object_or_404(Item, id=item_id)

And we also create an instance of our item form and return it to the template in the context.

form = ItemForm()
context = {
'form': form
}
return

6. We also want to form to be pre-populated with the current item data we pass an instance argument to the form. So within the brackets of
   form = ItemForm() we add:

- instance = item

which is telling it to populate it with the item data we just got from the database.

7. We need to import the get_object_or_404 at the top of views.py

8. The form is now on the Edit item page and it's pre-populated with the items data.
   But when we update it. It still doesn't actually update because we haven't written a post handler in the Edit item view.
   What we do is go to **views.py** and copy the entire handler from add_item view and only make small changes. We only add

- instance=item

after request.POST

if request.method == 'POST':
form = ItemForm(request.POST, instance=item)
if form.is_valid():
form.save()
return redirect('get_todo_list')

9. After this we should be able to update the items in the todo item list.

## Toggling and Deleting Items

### Toggling Items

To finally have 100% CRUD we will be giving the user is the ability to quickly toggle in items done status.
And then give them the ability to completely delete an item.

1.  We go to **todo_list.html** template and we copy the edit link part and just change the URL and the button text to toggle.

             <td>
                <a href="/toggle/{{ item.id }}">
                    <button>Toggle</button>
                </a>
            </td>

2.  We then go to **urls.py** and add:

- path('toggle/<item_id>', toggle_item, name='toggle'),

Don't forget to import toggle_item at the top of urls.py

3. Go to **views.py** and add:

- def toggle_item(request, item_id):
  item = get_object_or_404(Item, id=item_id)
  item.done = not item.done <-- This takes and flips the done status
  item.save() <--- before saving it again
  return redirect('get_todo_list')

4. We should now be able to toggle the done status of an item

### Deleting items

1. Go to **views.py** and copy the toggle_item view and change names to delete

def delete_item(request, item_id):
item = get_object_or_404(Item, id=item_id)
item.delete()
return redirect('get_todo_list')

2.  Then go to **urls.py** and copy the toggle_item url and change to delete_item

    path('delete/<item_id>', delete_item, name='delete')

3.  Finally we need to add one more button in the todo_list.html template

            <td>
                <a href="/delete/{{ item.id }}">
                    <button>Delete</button>
                </a>
            </td>

## Testing

When we create the todo app, there is automatically a file created called tests.py
In the file Django imports TestCase. This class is an extension of the Python standard library module called UnitTests.
Which provides us with a bunch of methods to assert various things about our code. Such as assert equal assert true assert false and so on.
Testing in most programming languages and frameworks is based on these assertions. And we'll use them to test our code in Django as well.

To get started we create a class called TestDjango which inherits the built in TestCase class.
Then assertEqual checks if 1 and 0 is the same.

class TestDjango(TestCase):

def test_this_thing_works(self): <--- All test names need to start with "test"
self.assertEqual(1, 0)

To run the test we write

- python3 manage.py test

We can also change the name of the test.py file to make it easier to sort the tests out from one another.
So I will rename this one \***\*test_views.py** and will also create **test_models.py** and **test_forms.py**

### Testing forms.py

I add this test to test item name is required.

class TestItemForm(TestCase):

    def test_item_name_is_required(self):
        form = ItemForm({'name': ''})
        self.assertFalse(form.is_valid())
        self.assertIn('name', form.errors.keys())
        self.assertEqual(form.errors['name'][0], 'This field is required.')

I'll begin by instantiating a form and we'll deliberately instantiate it without a name
to simulate a user who submitted the form without filling it out. This form should not be valid.
So I'll use \***\*assertFalse** to ensure that that's the case.
When the form is invalid it should also send back a dictionary of fields on which there were errors and the Associated error messages
Knowing this we can be even more specific by using \***\*assertIn** to assert
whether or not there's a name key in the dictionary of form errors. Finally to really drive the point home.
I'll use **assertEqual** to check whether the error message on the name field is this field is required.
Remember to include the period at the end here as the string will need to match exactly.
Also just a note we're using the zero index here because the form will return a list of errors on each field.
And this verifies that the first item in that list is our string telling us the field is required.

let's write another one to ensure the done field is not required.
It shouldn't be since it has a default value of false on the item model.
In this case we'll create the form sending only a name.
And then just test that the form is valid as it should be even without selecting a done status.
Finally let's assume that somewhere down the line another developer comes
along and changes the item model.
Adding a field to it that contains some sort of information we don't want to display on the form.
If you remember we actually defined the fields to display explicitly in the inner metaclass on the item form.
And the reason for that is otherwise the form will display all fields on the model
including those we might not want the user to see.

    def test_done_field_is_not_required(self):
        form = ItemForm({'name': 'Test Todo Item'})
        self.assertTrue(form.is_valid())

That said we should write a test to ensure that the only fields that are displayed in
the form are the name and done fields.
I'll call this test. test_fields_are_explicit_in_form_metaclass
For this test we can simply instantiate an empty form.
And then use assert equal to check whether the form.meta.fields attribute
is equal to a list with name and done in it.
This will ensure that the fields are defined explicitly.
And if someone changes the item model down the road our form won't
accidentally display information we don't want it to.
This will also protect against the fields being reordered. Since the list must match exactly.

def test_fields_are_explicit_in_forms_metaclass(self):
form = ItemForm()
self.assertEqual(form.Meta.fields, ['name', 'done'])

To test a specific test form use command:

- python3 manage.py test todo.test_forms

To test a specific class of tests:

- python3 manage.py test todo.test_forms.TestItemForm

Even run a specific individual test:

- python3 manage.py test todo.test_forms.TestItemForm.test_fields_are_explicit_in_form_metaclass

### Testing views.py

class TestViews(TestCase):

    def test_get_todo_list(self):

    def test_get_add_item_page(self):

    def test_get_edit_item_page(self):

    def test_can_add_item(self):

    def test_can_delete_item(self):

    def test_can_toggle_item(self):

The process here is going to be pretty straightforward.
We want to test not only that our views return a successful HTTP response
and that they're using the proper templates.
But also what they can do. Specifically adding toggling and deleting items.

To test the HTTP responses of the views.
We can use a built-in HTTP client that comes with the Django testing framework.
I'll start with the get_todo_list view.
By setting a variable response equal to self.client.get
And providing the URL slash since we just want to get the home page.
We can then use assert equal to confirm that the response.status code is equal to 200
A successful HTTP response.
To confirm the view uses the correct template.
I'll use self.assertTemplateUsed and tell it the template we expect it to use in the response.

    def test_get_todo_list(self):
        response = self.client.get('/')
        self.assertEqual(response.status_code, 200)
        self.assertTemplateUsed(response, 'todo/todo_list.html')

The Edit item page is a little different.
I'll paste in the same code and change the template we're expecting.
But, in this case, the URL will be edit followed by an item ID like 99 for example.
If we just pass it a static number though. The test will only pass if that item ID exists in our database.
And we want to be more generic than that.
Conveniently in Django tests, we can also do crud operations.
So let's import the item model at the top. And then create an item to use in this test.
Now that we've got the item created.
Testing that we can get the Edit URL.
Is as simple as adding on its ID. Which I'll do with the Python f string.
if you're not familiar with f strings.
They work almost identically to the template literals you learned about in the JavaScript lessons.
All we've got to do is add an f before the opening quotation mark.
And then anything we put in curly brackets will be interpreted and turned into part of the string.

Add at the top

- from .models import Item

  def test_get_edit_item_page(self):
  item = Item.objects.create(name='Test Todo Item')
  response = self.client.get(f'/edit/{item.id}') <---- Added so we get the specific item we want to test
  self.assertEqual(response.status_code, 200)
  self.assertTemplateUsed(response, 'todo/edit_item.html')

To test creating an item we can set the response equal to self.client.post on the add URL
And give it a name the item as if we've just submitted the item form.
If the item is added successfully. The view should redirect back to the home page.
So I'll use assert redirects. To confirm that it redirects back to slash.

    def test_can_add_item(self):
        response = self.client.post('/add', {'name': 'Test Added Item'})
        self.assertRedirects(response, '/')

Now let's test whether we can delete an item.
First I'll create one using item.objects.create.
And then I'll use the same syntax as we used on the edit_item view.
To make a get request. To delete slash the items ID
Again we'll want to assert that the view redirects us as that's what it should do if it's successful.
And while we should technically already know the test passed at this point.
Just to prove that the item is in fact deleted.
I'll try to get it from the database using .filter and passing it the item ID
Since that item is the only one on the database and we just deleted it.
We can be certain the view works by asserting whether the length of existing items is zero

def test_can_delete_item(self):
item = Item.objects.create(name='Test Todo Item')
response = self.client.get(f'/delete/{item.id}')
self.assertRedirects(response, '/')
existing_items = Item.objects.filter(id=item.id)
self.assertEqual(len(existing_items), 0)

Finally let's test whether toggling items is working.
The first three lines of this test will be almost the same.
So I'll copy those from above.
This time let's create an item with a done status of true. Then call the toggle URL on its ID.
After asserting that the view redirects us. We can get the item again.
And I'll call it updated item.
And then use assert false to check it's done status.
with that complete I'll run all the tests and verify that they all pass

    def test_can_toggle_item(self):
        item = Item.objects.create(name='Test Todo Item', done=True)
        response = self.client.get(f'/toggle/{item.id}')
        self.assertRedirects(response, '/')
        updated_item = Item.objects.get(id=item.id)
        self.assertFalse(updated_item.done)

NOTE: For some reason I failed on all tests that included tests where item was defined. To add "done=False" to the end of the item-variable solved this. This because the Item model in models.py, and specifically the done field does not accept null or blank.

To finally test how much of our code that we have actually tested there is a tool called coverage. We install it with

- pip3 install coverage

Then to run it, type:

- coverage run --source=todo manage.py test

And then to get a report:

- coverage report

or to get a more detailed report that will create a folder named "htmlcov"

- coverage html

and then

- python3 -m http.server

Then click on that htmlcov folder which will open an interactive version of the report.

## Heroku Setup

Since this video was created, the login command for heroku has changed. When the instructor logs in to heroku from the terminal, please use the following command:

- heroku login -i

This will no longer open up the login page in the browser, instead it will prompt you for your username and password in the terminal itself.

NOTE: In case you have Multi-Factor Authentication (MFA/2FA) enabled, you'll need a few extra steps:

    Click on Account Settings (via the avatar menu) on the Heroku Dashboard.
    Scroll down to the API Key section and click Reveal. Copy the key.
    Use the login command: heroku login -i
        Enter your Heroku username.
        Enter the API key you just copied when prompted for your password.

Before we actually deploy our project to Heroku. Let's set up some things it'll need in order to function out there in the wild.
First of all, you might remember that the db.sqlite3 file in the file explorer. Has been acting as our database throughout these videos.
This is fine for local development. But unfortunately, it won't work in production. Because Heroku uses an ephemeral file system.
Which means it's wiped clean every time Heroku runs updates. Or we redeploy our app. Because sqlite is a file-based database.
We'll lose our entire database every time this happens because when the file system is wiped the file will be deleted.
In general, you never want to store anything valuable on an ephemeral file system. Because it isn't guaranteed to stick around.
Instead, we'll use an add-on for Heroku. Which will allow us to use a server-based database called Postgres.
And that one will be separated from our application. So it'll survive even if the application server is destroyed.
To use Postgres in our application. We need to install a package called psycopg2 Which we can do with

- pip3 install psycopg2-binary

Later on, we'll add the Heroku add-on to set it up. But this will take care of the Django side.
We'll also need a package called gunicorn. Or green unicorn. Which will replace our development server once the app is deployed to Heroku.
Gunicorn will act as our web server. And we can install it using

- pip3 install gunicorn

With those two packages installed. I'm going to use a new command

- pip 3 freeze - - local > requirements.txt

And will direct it into a file called requirements .txt This requirements file is how Heroku will know what it needs to install for our app to work.
Specifically, it'll tell Heroku all the packages it needs to install using pip.


Now that we've got a requirements file and have installed everything our project will need to run on Heroku.
We can actually create the Heroku app itself. 
To create an app. i'll use the command 

- Heroku create cg-django-todo-app

But you can name it whatever you want. You can also specify a region using the --region flag
By default, the app will be created in the us region. But if you're in the European union you can simply specify --region eu
With the app created. You should now be able to see it in the list when you run the command Heroku apps.

It should now be created and if you write

- heroku apps

I see a list of all apps I currently have on Heroku

Going forward we're going to use a tool called git. To manage different versions of our app.
And handle deploying it to Heroku.
Git is a version control system. That'll allow us to track changes to our code over time
Similar to being able to save your progress in a video game.
When we create a Heroku app.
It automatically sets up a git repository for us that we can push our code changes to.
And this is how we'll deploy our project.
If you type git 

- remote -v (for verbose.)
You'll see that there are two key remote urls here. One for pushing code to Heroku. And one for fetching code from Heroku.
This tells us that when we use the command 

- git push heroku master

It will be pushed to the master branch at this url.
If we use the command 

- git push origin master

It would go to the other remote url

## Create a Database

As your database is currently hosted on Heroku, you will need to move your data out of it. So first, we will create a new database with a free service at ElephantSQL.

1. Log in to ElephantSQL.com to access your dashboard

2. Click “Create New Instance”

3. Set up your plan
    - Give your plan a Name (this is commonly the name of the project)
    - Select the Tiny Turtle (Free) plan
    - You can leave the Tags field blank

4. Select “Select Region”

5. Select a data center near you

6. Then click “Review”

7. Check your details are correct and then click “Create instance”

8. Return to the ElephantSQL dashboard and click on the database instance name for this project

9. Copy the database url for your project, as we’ll need it in the next step

That’s the database created, but how do we connect it to our new deployed app? 

## Connecting the Database to Our App

we set up a new external database for use on our deployed project. Next, we will need to create the Heroku app and add the DATABASE_URL Config Var so our Heroku app can connect to it.

### Creating the Heroku app

First we need to create this new app where our project will be hosted. You’ve done this in previous projects, but as a reminder, here are the steps:

1. Log in to your Heroku account

2. Click the New button in the top right corner

3. Choose a name for your project. This must be unique. Select the region closest to you. Confirm by clicking Create app

### Adding the DATABASE_URL Config Var

1. Go to the Settings tab

2. Click Reveal Config Vars

3. Add a Config Var called DATABASE_URL. Paste your ElephantSQL database URL in as the value

Great, we now have our app set up on Heroku and it is connected to our external database. We need to do one more thing before we can go back to the videos, and that is to connect our IDE workspace to the external database so we can migrate the models.

### Hello Django: Connecting the external database to your IDE

Now we’ll connect our new database to our workspace, so we can migrate our models to the new database and get it working like our local one did.

### Process

1. In your env.py file add a new key, DATABASE_URL, and give it a value of the copied database URL.

-  os.environ.setdefault("DATABASE_URL", "my_copied_database_url")

2. Install the dj-database-url package version 0.5.0 in the terminal with pip3. This will allow us to parse the URL we got above to a format Django can work with:

-  pip3 install dj_database_url==0.5.0

and remember to add it to your requirements.txt with

- pip3 freeze --local > requirements.txt

3. At the top of settings.py, import the package and the env.py file

 from pathlib import Path
 import os
 import dj_database_url
 import env

4. In settings.py, comment out the default database setting and replace it to use the DATABASE_URL environment variable. Your code should now look like this

"""
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': BASE_DIR / 'db.sqlite3',
    }
}
"""

DATABASES = {
    'default' : dj_database_url.parse(os.environ.get('DATABASE_URL'))
}

5. Run the migrate command in the terminal to build the database according to the model structure we created in earlier videos

-  python3 manage.py migrate

Note: this does not transfer the data, only the database structure.

6. Run the project to test everything is connected, and add in a few items for your to-do list. 

NOTE: For security reasons, please do not commit your code with the external database URL visible in the settings.py file. You can use an env.py file to hide it now if you want to. In case you need a reminder of how to do this, you can find the steps in the banner above the next video.

If it happens like it just did to me. You need to rotate password in the app settings in elephantSQL, then change to the new database URL in both env.py and Config Vars in Heroku.

Keep in mind that whenever we mention the Heroku Postgres database from this point forward, this is our external database on ElephantSQL.

please create an env.py and add a new environment variable called DATABASE_URL. In case you need a reminder, you can find the steps for this below the video.

Reminder: The env.py file must be added to the .gitignore. If you are using the CI full template, it should already be there.

