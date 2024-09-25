## 70. How do you interact with a REST API using Python?


Interacting with a REST API in Python is commonly done using the `requests` library. This library provides a simple and elegant way to send HTTP requests to interact with RESTful web services. Below are the steps and examples of how to interact with a REST API using Python.

### 1. **Install the `requests` Library**

If you don't already have the `requests` library installed, you can install it using pip:

```bash
pip install requests
```

### 2. **Making Basic HTTP Requests**

The basic HTTP methods used to interact with REST APIs are:

- **GET:** Retrieve data from the server.
- **POST:** Submit data to the server.
- **PUT:** Update existing data on the server.
- **DELETE:** Remove data from the server.

### 3. **Sending a GET Request**

A GET request is used to retrieve data from a server. 

**Example:**

```python
import requests

# Sending a GET request
response = requests.get('https://jsonplaceholder.typicode.com/posts')

# Check if the request was successful
if response.status_code == 200:
    # Parse the JSON data
    data = response.json()
    for post in data:
        print(f"Title: {post['title']}")
else:
    print(f"Failed to retrieve data: {response.status_code}")
```

- **Explanation:** The `requests.get()` function sends a GET request to the specified URL. The `response.json()` method parses the JSON response into a Python dictionary or list.

### 4. **Sending a POST Request**

A POST request is used to submit data to the server, such as creating a new resource.

**Example:**

```python
import requests

# Data to be sent to the API
data = {
    'title': 'foo',
    'body': 'bar',
    'userId': 1
}

# Sending a POST request
response = requests.post('https://jsonplaceholder.typicode.com/posts', json=data)

# Check if the request was successful
if response.status_code == 201:
    print(f"Created new resource: {response.json()}")
else:
    print(f"Failed to create resource: {response.status_code}")
```

- **Explanation:** The `requests.post()` function sends a POST request with the `data` dictionary serialized to JSON using the `json` parameter. A successful POST request typically returns a `201` status code.

### 5. **Sending a PUT Request**

A PUT request is used to update existing data on the server.

**Example:**

```python
import requests

# Data to update
data = {
    'id': 1,
    'title': 'updated title',
    'body': 'updated body',
    'userId': 1
}

# Sending a PUT request
response = requests.put('https://jsonplaceholder.typicode.com/posts/1', json=data)

# Check if the request was successful
if response.status_code == 200:
    print(f"Updated resource: {response.json()}")
else:
    print(f"Failed to update resource: {response.status_code}")
```

- **Explanation:** The `requests.put()` function sends a PUT request with the updated data. This is typically used to update a resource at a specific URL.

### 6. **Sending a DELETE Request**

A DELETE request is used to remove data from the server.

**Example:**

```python
import requests

# Sending a DELETE request
response = requests.delete('https://jsonplaceholder.typicode.com/posts/1')

# Check if the request was successful
if response.status_code == 200:
    print("Resource deleted successfully.")
else:
    print(f"Failed to delete resource: {response.status_code}")
```

- **Explanation:** The `requests.delete()` function sends a DELETE request to the specified URL. A successful deletion typically returns a `200` or `204` status code.

### 7. **Handling Query Parameters**

You can pass query parameters to a GET request using the `params` parameter.

**Example:**

```python
import requests

# Define query parameters
params = {
    'userId': 1
}

# Sending a GET request with query parameters
response = requests.get('https://jsonplaceholder.typicode.com/posts', params=params)

if response.status_code == 200:
    data = response.json()
    print(data)
else:
    print(f"Failed to retrieve data: {response.status_code}")
```

- **Explanation:** The `params` dictionary is passed to the `requests.get()` function, which appends them to the URL as query parameters.

### 8. **Handling Headers**

You can pass custom headers to a request using the `headers` parameter.

**Example:**

```python
import requests

# Define headers
headers = {
    'Authorization': 'Bearer your_token_here',
    'Content-Type': 'application/json'
}

# Sending a GET request with custom headers
response = requests.get('https://jsonplaceholder.typicode.com/posts', headers=headers)

if response.status_code == 200:
    data = response.json()
    print(data)
else:
    print(f"Failed to retrieve data: {response.status_code}")
```

- **Explanation:** The `headers` dictionary is passed to the request, allowing you to specify custom HTTP headers.

### 9. **Handling Errors**

You can check the status code of the response to handle errors gracefully.

**Example:**

```python
import requests

response = requests.get('https://jsonplaceholder.typicode.com/invalid-url')

try:
    response.raise_for_status()
except requests.exceptions.HTTPError as err:
    print(f"HTTP error occurred: {err}")
except Exception as err:
    print(f"Other error occurred: {err}")
else:
    print("Success!")
```

- **Explanation:** The `raise_for_status()` method raises an exception for HTTP error codes (4xx or 5xx). You can catch these exceptions to handle them appropriately.

### Summary

- **GET:** Retrieve data using `requests.get()`.
- **POST:** Submit data using `requests.post()`.
- **PUT:** Update data using `requests.put()`.
- **DELETE:** Remove data using `requests.delete()`.
- **Query Parameters:** Pass query parameters using the `params` argument.
- **Headers:** Pass custom headers using the `headers` argument.
- **Error Handling:** Use `response.raise_for_status()` to handle HTTP errors.

The `requests` library is a powerful and user-friendly way to interact with REST APIs in Python, making it easy to send HTTP requests and handle responses.