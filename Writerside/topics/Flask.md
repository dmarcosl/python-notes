# Flask

Flask is a lightweight web framework to build web applications quickly.

## Setting up a Flask project

Install Flask with pip:

```bash
pip install Flask
```

Create a new file `app.py` and write the following code to set up a basic Flask application:

```python
from flask import Flask

app = Flask(__name__)

@app.route('/')
def hello_world():
    return 'Hello, World!'

if __name__ == '__main__':
    app.run(debug=True)
```

Then run the app using:

```bash
python app.py
```

The application will run on [http://127.0.0.1:5000/](http://127.0.0.1:5000/).

## Routing and handling requests

Routes in Flask define the endpoints of the application.

You can use decorators to specify which function handles which URL.

Example:

```python
@app.route('/submit', methods=['POST'])
def submit():
    data = request.form['field_name']
    return f'Form data: {data}'
```

## Working with templates (Jinja2)

Flask uses Jinja2 as the templating engine to render HTML. Jinja2 allows you to dynamically generate HTML content from templates.

Create an HTML template `index.html`:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Hello {{ name }}</title>
</head>
<body>
    <h1>Hello, {{ name }}!</h1>
</body>
</html>
```

Render it from Flask:

```python
from flask import render_template

@app.route('/greet/<name>')
def greet(name):
    return render_template('index.html', name=name)
```

## Handling forms and requests data

Flask easily handles form data using `request.form` for POST requests.

Example:

```python
from flask import request

@app.route('/submit', methods=['POST'])
def submit():
    username = request.form['username']
    return f'Username: {username}'
```

You can also handle query parameters in a URL with request.args:

```python
@app.route('/search')
def search():
    query = request.args.get('q')
    return f'Search results for: {query}'
```

## Using Flask extensions: Flask-SQLAlchemy

Flask extensions add extra functionality to Flask applications.

Flask-SQLAlchemy allows ORM-based database integration.

```python
from flask_sqlalchemy import SQLAlchemy

app.config['SQLALCHEMY_DATABASE_URI'] = 'sqlite:///site.db'
db = SQLAlchemy(app)

class User(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    username = db.Column(db.String(100), unique=True, nullable=False)

@app.route('/add_user', methods=['POST'])
def add_user():
    new_user = User(username=request.form['username'])
    db.session.add(new_user)
    db.session.commit()
    return f'User {new_user.username} added!'
```

## Using Flask extensions: Flask-WTF

Flask-WTF allows to handle forms with validation.

```python
from flask_wtf import FlaskForm
from wtforms import StringField
from wtforms.validators import DataRequired

class MyForm(FlaskForm):
    name = StringField('Name', validators=[DataRequired()])

@app.route('/form', methods=['GET', 'POST'])
def form():
    form = MyForm()
    if form.validate_on_submit():
        return f'Hello, {form.name.data}!'
    return render_template('form.html', form=form)
```

## Error handling and logging in Flask

Flask allows to manage errors and log important application events.

To handle specific HTTP errors, use error handlers:

```python
import logging

app.logger.setLevel(logging.DEBUG)

@app.errorhandler(404)
def not_found(error):
    app.logger.debug('Error 404')
    return 'This page does not exist!', 404
```

## Deployment of Flask applications

Flask is not intended to be used directly in production. To deploy it to production you must use WSGI servers like Gunicorn or uWSGI.

Install Gunicorn

```bash
pip install gunicorn
```

Run it:

```bash
gunicorn app:app
```