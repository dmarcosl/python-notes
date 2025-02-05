# FastAPI

FastAPI is a high-performance web framework for building APIs, designed for asynchronous operations.

It simplifies creating RESTful APIs with automatic data validation and OpenAPI documentation.

## Introduction to FastAPI

Install FastAPI and an asynchronous WSGI server

```bash
pip install fastapi uvicorn
```

Create a new file `app.py` and write the following code to set up a basic FastAPI application:

```python
from fastapi import FastAPI

app = FastAPI()

@app.get('/')
def read_root():
    return {'message': 'Hello, World!'}
```

Then run the app using:

```bash
uvicorn app:app --reload
```

## Setting up routes and handling requests

Routes in FastAPI define the API endpoints.

Request data can be accessed using path parameters, query parameters, and request bodies.

```python
@app.get('/greet/{name}')
def greet(name: str):
    return {'message': f'Hello, {name}!'}
```

## Dependency injection and middleware

FastAPI supports dependency injection to manage shared resources such as database connections, authentication, etc.

You can define dependencies and inject them into routes.

```python
from fastapi import Depends

def get_db():
    db = 'Database Connection'  # Example dependency
    return db

@app.get('/items')
def get_items(db: str = Depends(get_db)):
    return {'db': db}
```

Middleware allows you to handle requests and responses globally.

It’s useful for tasks like logging, CORS handling, etc.

```python
from fastapi import FastAPI
from starlette.middleware.base import BaseHTTPMiddleware

class CustomMiddleware(BaseHTTPMiddleware):
    async def dispatch(self, request, call_next):
        response = await call_next(request)
        response.headers['X-Custom-Header'] = 'Value'
        return response

app.add_middleware(CustomMiddleware)
```

## Validating request data using Pydantic models

FastAPI uses Pydantic models to validate incoming data, ensuring that the correct data types are received.

You define Pydantic models to specify the structure of the data expected.

```python
from pydantic import BaseModel

class Item(BaseModel):
    name: str
    price: float

@app.post('/items/')
def create_item(item: Item):
    return {'name': item.name, 'price': item.price}
```

FastAPI automatically validates the input data based on the `Item` model and generates an error response if the data is invalid.

## Asynchronous support with FastAPI

FastAPI supports asynchronous programming using `async` and `await`.

This allows you to handle non-blocking I/O operations efficiently, such as database queries, file handling, or HTTP requests.

```python
@app.get('/async-items/')
async def get_items():
    await asyncio.sleep(1)  # Simulate async task
    return {'items': ['item1', 'item2']}
```

## FastAPI authentication mechanisms

FastAPI offers authentication mechanisms with OAuth2 and JWT for securing the API.

These can be easily integrated with FastAPI's built-in tools.

Example:

```python
from fastapi import Depends, HTTPException
from fastapi.security import OAuth2PasswordBearer
import jwt

oauth2_scheme = OAuth2PasswordBearer(tokenUrl='token')

def verify_token(token: str = Depends(oauth2_scheme)):
    try:
        payload = jwt.decode(token, 'secret', algorithms=['HS256'])
        return payload
    except jwt.ExpiredSignatureError:
        raise HTTPException(status_code=401, detail='Token expired')
    except jwt.InvalidTokenError:
        raise HTTPException(status_code=401, detail='Invalid token')

@app.get('/protected/')
def protected_route(token: str = Depends(verify_token)):
    return {'message': 'You are authorized', 'token_data': token}
```

## Generating OpenAPI Documentation

FastAPI automatically generates OpenAPI documentation based on the Python code, providing an interactive UI where users can explore and test the API.

To access the documentation, start the app and visit `/docs` or `/redoc` for alternative documentation formats:

```bash
uvicorn app:app --reload
```

Go to [http://127.0.0.1:8000/docs](http://127.0.0.1:8000/docs) for the interactive Swagger UI or [http://127.0.0.1:8000/redoc](http://127.0.0.1:8000/redoc) for ReDoc documentation.

You can also export the OpenAPI spec from FastAPI by visiting [http://127.0.0.1:8000/openapi.json](http://127.0.0.1:8000/openapi.json).