Lets take this form
```html
<form action="/login" method="POST">
  <input type="text" name="username">
  <input type="password" name="password">
  <button type="submit">Login</button>
</form>

```


| Attribute              | Meaning                                         |
| ---------------------- | ----------------------------------------------- |
| `action="/login"`      | Send the request to this URL (your Flask route) |
| `method="POST"`        | Use HTTP **POST method** to send data           |
| `button type="submit"` | Triggers the request                            |
- **Browser collects** the input values (e.g., username and password)
- It **creates a POST request** to the URL in the `action` (e.g., `/login`)
- That request goes to your **Flask backend** at this route:

```python
@app.route("/login", methods=["POST"])
def login():
    username = request.form["username"]
    password = request.form["password"]
    return f"Logged in as {username}"
```


For **GET**
```python 
@app.route("/feed", methods=["GET"])
def get_feed():
    data = [
        {"user": "mounesh", "msg": "Hello"},
        {"user": "kumar", "msg": "API learning!"}
    ]
    return jsonify(data)
```
