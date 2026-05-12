---
tags: ["python", "tools", "requests", "http", "curl"]
---
# Python requests vs curl

Side-by-side equivalents for the most common `curl` patterns using the `requests` library.

## Dependencies

```bash
pip install requests
```

## Code

### GET

```bash
# curl
curl https://api.example.com/users
```

```python
import requests

response = requests.get("https://api.example.com/users")
print(response.json())
```

### POST (form data)

```bash
# curl
curl -X POST -d "name=test" https://api.example.com/users
```

```python
response = requests.post("https://api.example.com/users", data={"name": "test"})
```

### POST (JSON body)

```bash
# curl
curl -X POST \
  -H "Content-Type: application/json" \
  -d '{"name":"test"}' \
  https://api.example.com/users
```

```python
response = requests.post("https://api.example.com/users", json={"name": "test"})
```

### Custom headers

```bash
# curl
curl -H "Authorization: Bearer TOKEN" \
     -H "Content-Type: application/json" \
     https://api.example.com/protected
```

```python
headers = {
    "Authorization": "Bearer TOKEN",
    "Content-Type": "application/json",
}
response = requests.get("https://api.example.com/protected", headers=headers)
```

### Send cookies

```bash
# curl
curl -b "session=abc123; user=john" https://api.example.com/dashboard
```

```python
cookies = {"session": "abc123", "user": "john"}
response = requests.get("https://api.example.com/dashboard", cookies=cookies)
```

### Skip TLS verification (`-k`)

```python
response = requests.get("https://self-signed.example.com", verify=False)
```
