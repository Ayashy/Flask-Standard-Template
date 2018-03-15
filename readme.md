

** Basic Structure

website
    app
        templates
            index.html
            base.html
        __init__.py
        models.py
        routes.py
    migrations
    website.py
    config.py
    forms.py

** TEMPLATE SYNTAXE

* This is the syntaxe for jinja that alows code in views

{{ var }}   : for variable access (render argument)
{% if %} {% else %}     : Conditional block
{% For %} {% endfor %}  : Loop block
{% extends "base.html" %}   : Template heritage
{% block content %} {% endblock %}  : Content block


** CONFIGURATION

* You can add variables as keys in app.config

app.config['SECRET_KEY'] = 'you-will-never-guess'

* Or use a class to store configuration variables

config.py
app.config.from_object(Config)

** WTF FORMS

- Used to generate forms automatically
- uses the packages flask-wtf

* Create the form class

- The class inherits from FlaskForm
- Form classes best put in a separate package
- You need to implement each field of the form

* Create the form view

- An instance of the form class must be passed as an argument to the view
- Use the class to 
- {{ form.hidden_tag() }}   : used to protect from an attack (uses the secret key)
- {{ form.username.label }}
- {{ form.username(size=32) }} 
- Additional arguments can be passed to the forms ( like css and html properties)

* Receiving form data

- You can callback the same form and check if its a response
- form.validate_on_submit()

** FLASK FEATURES

* Flash messages

- Its a buffer of messages that can be consumed to show them on the pages
- flash() adds a message to the queu
- get_flashed_messages() consumes all the messages and clears the buffer


** DATABASE

* Extensions

- Flask_sqlAlchemy is a wrapper around sqlalchemy
- sqlAlchemy is an ORM for python. It's compatible with multple databases
- Flask-Migrate is an extension for managing database migrations based on the alembic framework

* Configuration 

- SQLALCHEMY_DATABASE_URI   : to configure database location
- SQLALCHEMY_TRACK_MODIFICATIONS    : to disable modification changes
- db = SQLAlchemy(app) and migrate = Migrate(app, db) to use the database and migration objects
- Relationships are implemented using foreign key and db.relationship() (for list of items)

* Creating models

- Models classes must inherit from db.model
- Data is implemented as db.Column
- Can implement __repr__ for visualisation

* Migrations 

- flask db init : Creates the migration directory
- flask db migrate -m "users table" : to create a new migration for the current DB schema
- flask db upgrade/downgrade    : to apply/remove migrations

* Manipulating data

- Use the SQLAlchemy doc to check for syntaxe
- db.session.add()  : for adding a new object
- db.session.delete(u)  : to delete an item u
- User.query.all()  : to get list of User entries
- db.session.commit() : to commit the changes

** FLASK-LOGIN

* Configuration

- login = LoginManager(app) : to initialize the instance
- Must configure the user model accordingly
    is_authenticated: check valid credentials
    is_active: check if account is active
    is_anonymous: true for special anonymous users
    get_id(): unique identifier for the user as a string 
- You can inherit from UserMixin class as a generic implementation
- Implement a @login.user_loader function in the model

* Request loggin

- Set up login.login_view = 'login' in __init__.py
- Use decorator @login_required
- Redirect to previous page using the "next" parameter


* Registration form

- Create the registration form


