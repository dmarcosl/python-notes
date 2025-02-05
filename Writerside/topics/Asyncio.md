# Asyncio

`asyncio` is a standard library for writing concurrent programs using the `async`/`await` syntax.

It allows running multiple tasks concurrently without needing multiple threads or processes.

Instead of using threads, asyncio utilizes a single thread and an event loop to manage concurrent tasks.

## Using asyncio for concurrent execution

```python
import asyncio

async def task1():
    print('Task 1 started')
    await asyncio.sleep(2)
    print('Task 1 completed')

async def task2():
    print('Task 2 started')
    await asyncio.sleep(1)
    print('Task 2 completed')

async def main():
    await asyncio.gather(task1(), task2())

# Running the event loop
asyncio.run(main())
```

In this example, `task1()` and `task2()` run concurrently, and the event loop handles both tasks.

## Writing asynchronous functions

Asynchronous functions in Python are defined using `async def`, instead of `def`, allowing the use of `await` within the function to pause its execution and wait for results from other asynchronous tasks.

The `await` keyword allows other tasks to execute while waiting.

Example:

```python
async def fetch_data():
    print('Fetching data...')
    await asyncio.sleep(2)  # Simulating an I/O operation
    print('Data fetched')
    return 'Data'

async def main():
    result = await fetch_data()
    print(result)

asyncio.run(main())
```

## Managing event loops and background tasks

### Event Loop

The event loop in `asyncio` is responsible for managing asynchronous tasks.

Python has a default event loop that can be used to run multiple tasks concurrently.

It's important to manage it properly, especially when using web frameworks like Flask or FastAPI that have their own event loops.

Example of a manual event loop:

```python
import asyncio

async def task():
    await asyncio.sleep(1)
    print('Task complete')

loop = asyncio.get_event_loop()
loop.run_until_complete(task())
```

### Background Tasks

In web applications, it is common to run background tasks.

You can manage these tasks in Flask or FastAPI using asyncio.

Example with FastAPI:

```python
from fastapi import FastAPI, BackgroundTasks

app = FastAPI()

def background_task(name: str):
    print(f'Hello {name}, this is a background task.')

@app.get('/')
async def hello(background_tasks: BackgroundTasks):
    background_tasks.add_task(background_task, 'FastAPI User')
    return {'message': 'Task is running in the background'}
```

## Running asynchronous tasks in Flask

Flask does not have built-in support for asynchronous tasks, but you can use asyncio to run tasks in the background. It is important to run asynchronous functions inside an event loop.

Example:

```python
from flask import Flask
import asyncio

app = Flask(__name__)

async def background_task():
    await asyncio.sleep(3)
    return 'Task completed'

@app.route('/')
async def index():
    task = asyncio.create_task(background_task())
    await task
    return 'Task executed in background'

if __name__ == '__main__':
    app.run(debug=True)
```

## Running asynchronous tasks in FastAPI

FastAPI supports asynchronous functions natively thanks to its integration with asyncio.

Routes can be defined with `async def`, allowing tasks to run concurrently.

```python
from fastapi import FastAPI
import asyncio

app = FastAPI()

async def background_task():
    await asyncio.sleep(3)
    return 'Task completed'

@app.get('/')
async def root():
    task = asyncio.create_task(background_task())
    await task
    return {'message': 'Task executed in background'}
```