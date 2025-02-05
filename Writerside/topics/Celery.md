# Celery

Celery is a framework that allows the creation and management of asynchronous tasks. It supports executions at a certain time or periodically.

It is composed by three actors:

- The **beater**, which schedules the task at the defined time or at the end of the selected interval that has been specified
- The **worker**, which executes the scheduled tasks
- The **message broker**, an external application to share messages between both. It can be Redis, RabbitMQ, MongoDB, Kafka, etc

## Setting up Celery

To use Celery, you must have already a message broker configured.

First install Celery

```bash
pip install celery
```

Create a new file `app.py` and write the following code to set up a basic Celery application

```python
from celery import Celery

celery_app = Celery('tasks', broker='redis://localhost:6379/0', backend='redis://localhost:6379/0')
```

Worker execution

```bash
celery worker -A app.celery_app --loglevel=info
```

Beater execution

```bash
celery beat -A app.celery_app --loglevel=info
```

Remove all scheduled tasks

```bash
celery purge -A app.celery_app
```

## Asynchronous task execution

Celery allows to execute tasks asynchronously.

Once a task is submitted, the worker processes it in the background, freeing the main process to handle other requests.

```python
@celery_app.task(name='scheduled_task')
def scheduled_task(text):
    return text

@celery_app.task(name='periodic_task')
def periodic_task():
    return 'Task completed'

@celery_app.on_after_configure.connect
def setup_periodic_tasks(sender, **kwargs):
    sender.add_periodic_task(crontab(minute=0, hour=6, day_of_week=4), scheduled_task.s('hello world'))  # execute the Thursday at 06.00
    sender.add_periodic_task(10.0, periodic_task.s())  # execute every 10 seconds
```

## Task retries and failure handling

Celery supports automatic retries for tasks.

You can configure the number of retries and backoff intervals in case of task failure.

```python
@celery.task(bind=True, max_retries=3)
def some_task_with_retry(self):
    try:
        pass
    except Exception as exc:
        raise self.retry(exc=exc, countdown=60)  # Retry after 60 seconds
```

## Using Redis as message broker

The configuration is set through the broker URL in Celery's setup:

```python
celery_app = Celery(
    'tasks', 
    broker='redis://localhost:6379/0', 
    backend='redis://localhost:6379/0'
)
```

## Using RabbitMQ as message broker

To configure RabbitMQ, change the broker URL:

```python
celery = Celery(
    'tasks', 
    broker='pyamqp://guest@localhost//', 
    backend='redis://localhost:6379/0'
)
```

## Using Kafka as message broker

While not as commonly used as Redis or RabbitMQ, Celery can integrate with Kafka for message brokering.

You will need the `celery[redis]` and `celery[kafka]` extra dependencies installed:

```bash
pip install celery[kafka]
```

Then, configure the broker as follows:

```python
celery = Celery(
    'tasks', 
    broker='kafka://localhost:9092', 
    backend='redis://localhost:6379/0'
)
```

## Integrating Celery with Flask

You can integrate Celery with Flask by configuring the Celery object with the Flask app and initializing it.

Example:

```python
from celery import Celery
from flask import Flask

app = Flask(__name__)

def make_celery(app):
    celery = Celery(
        app.import_name, 
        backend=app.config['CELERY_RESULT_BACKEND'],
        broker=app.config['CELERY_BROKER_URL']
    )
    celery.conf.update(app.config)
    return celery

app.config.update(
    CELERY_BROKER_URL='redis://localhost:6379/0',
    CELERY_RESULT_BACKEND='redis://localhost:6379/0'
)

celery = make_celery(app)
```

## Integrating Celery with FastAPI

FastAPI integrates with Celery similarly. You need to configure Celery as a background task manager and start the worker to handle tasks.

Example:

```python
from celery import Celery
from fastapi import FastAPI

app = FastAPI()

celery = Celery(
    'tasks', 
    broker='redis://localhost:6379/0', 
    backend='redis://localhost:6379/0'
)

@app.post("/background_task/")
def background_task():
    celery.send_task('tasks.some_long_task')
```