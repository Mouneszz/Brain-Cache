Flask is a lightweight Python web framework used to build web applications. It helps you:
- Create routes (URLs)
- Handle HTTP methods (GET, POST)
- Connect with databases
- Render HTML using Jinja templates


### **Basic Setup for Flask and DB**
```python
from flask import Flask, render_template, request, redirect
from flask_sqlalchemy import SQLAlchemy

app = Flask(__name__)
app.config['SQLALCHEMY_DATABASE_URI'] = 'mysql+mysqlconnector://root:password@localhost/todoapp'
app.config['SQLALCHEMY_TRACK_MODIFICATIONS'] = False
db = SQLAlchemy(app)
```

### **Model Creation for Database**
```python
class Mytask(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    content = db.Column(db.String(100), nullable=False)
    complete = db.Column(db.Boolean, default=False)
    created = db.Column(db.DateTime, default=db.func.current_timestamp())
```

### **Create A Route**
```python 
@app.route("/", methods=["POST", "GET"])
def index():
    if request.method == "POST":
        task_content = request.form["content"]
        new_task = Mytask(content=task_content)
        db.session.add(new_task)
        db.session.commit()
        return redirect("/")
    else:
        tasks = Mytask.query.order_by(Mytask.created).all()
        return render_template("index.html", tasks=tasks)
```
🧠 **What happens here**:
- `GET` (when you visit `/`):
    - Fetch all tasks and render HTML
        
- `POST` (when you submit form):
    - Add task to DB and redirect to `/`

### **HTML with jinja**
```html
<!DOCTYPE html>
<html>
<head>
  <title>Todo App</title>
</head>
<body>
  <h1>Todo List</h1>
  <form method="POST" action="/">
    <input type="text" name="content" placeholder="Enter a task">
    <input type="submit" value="Add Task">
  </form>

  <ul>
    {% for task in tasks %}
      <li>{{ task.content }} - {{ task.created.strftime('%Y-%m-%d') }}</li>
    {% endfor %}
  </ul>
</body>
</html>
```

- `{% ... %}` → Logic (loops, if-else)
    
- `{{ ... }}` → Print values (like variables)