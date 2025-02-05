# Requests

The `requests` library simplifies HTTP requests, making it easy to interact with web APIs and retrieve web content.

## Installing Requests

```bash
pip install requests
```

## Making HTTP Requests

- `requests.get(url)`: Sends a GET request to retrieve data. 
- `requests.post(url, data={})`: Sends a POST request with data. 
- `requests.put(url, data={})`: Updates a resource. 
- `requests.delete(url)`: Deletes a resource.

Example:

```python
import requests

response = requests.get('https://example.com')
print(response.content)
```

## Handling Query Parameters

Use `params` to send query parameters in a request.

Example:

```python
payload = {'userId': 1}
response = requests.get('https://example.com', params=payload)
print(response.url)
```

Output:

```Plain Text
https://example.com/?userId=1
```

## Sending JSON Data in a POST Request

Example:

```python
data = {'title': 'New Post', 'body': 'Content', 'userId': 1}
response = requests.post('https://example.com', json=data)
print(response.status_code, response.content)
```

## Handling Headers and Authentication

Example:

```python
headers = {'Authorization': 'Bearer your_token'}
response = requests.get('https://example.com', headers=headers)
```

## Downloading Files

Example:

```python
response = requests.get('https://example.com/image.jpg')
with open('image.jpg', 'wb') as file:
    file.write(response.content)
```

## Response Attributes and Methods

The `requests.Response` object provides attributes and methods to handle HTTP responses efficiently.

- `.status_code`: Returns the HTTP status code.
- `.headers`: Retrieves response headers as a `dict`.
- `.url`: Shows the final URL after redirections.
- `.elapsed`: Time taken for the request.
- `.text`: Decodes response content as a string.
- `.content`: Returns raw binary content.
- `.json()`: Parses response as JSON.
- `.history`: Shows redirection history.
- `.encoding`: Gets/sets encoding for .text.

Example:

```python
response = requests.get('https://example.com')
print(response.status_code)              # 200
print(response.headers['Content-Type'])  # application/json; charset=utf-8
print(response.url)                      # Final URL
print(response.elapsed)                  # Response time
print(response.text)                     # Returns the response as a string
print(response.content)                  # Returns raw bytes
print(response.json())                   # Parses JSON response
print(response.history)                  # List of previous responses
print(response.encoding)                 # Default encoding (usually utf-8)
```

## Error Handling

Use `response.raise_for_status()` to handle HTTP errors.

Example:

```python
try:
    response = requests.get('https://example.com/error')
    response.raise_for_status()
except requests.exceptions.RequestException as e:
    print(f'Error: {e}')
```