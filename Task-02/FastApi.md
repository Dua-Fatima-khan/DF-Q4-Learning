
# FastAPI - Getting Started with APIs

Welcome to **Task 02** of your journey into building AI-powered web apps!  
In this task, you'll learn how to create your first **FastAPI application** — a modern and fast way to build APIs using Python.

>  No need for Postman or advanced tools — just your browser and code editor!

---

## 📦 What is an API?

An **API (Application Programming Interface)** is like a waiter in a restaurant:

- You tell the waiter what you want (your request).
- The waiter takes your request to the kitchen (the server).
- Then brings back what you asked for (the response).

In programming, APIs help different software talk to each other.

---

## What is FastAPI?

**FastAPI** is a Python tool that helps you build APIs quickly and easily. It’s:

- Very fast
- Smart (auto-detects data types)
- Comes with automatic documentation
- Great for beginners who know basic Python

---

## 🛠️ Step-by-Step: Your First FastAPI App

### 1. **Install FastAPI & Uvicorn**

Open your terminal and install these two packages:

```bash
pip install fastapi uvicorn
```

- `fastapi`: The main framework
- `uvicorn`: A server to run your app

---

### 2. **Create a File Called `main.py`**

This will be your main app file.

Paste this code inside it:

```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
def read_root():
    return {"message": "Hello Fatima! 🌸"}
```

Let’s break this down:

| Line | What it does |
|------|--------------|
| `from fastapi import FastAPI` | Import FastAPI package |
| `app = FastAPI()` | Create an app instance |
| `@app.get("/")` | Define a route (homepage) |
| `def read_root():` | Function to run when someone visits `/` |
| `return { ... }` | Send back a message as JSON |

---

### 3. **Run Your App**

In your terminal, run:

```bash
uvicorn main:app --reload
```

- `main`: name of your file (`main.py`)
- `app`: the FastAPI instance we created
- `--reload`: auto-restarts the server when you save changes

You’ll see something like:

```
INFO:     Uvicorn running on http://127.0.0.1:8000
```

---

### 4. **See Your App in Action!**

Open your browser and go to:

👉 [http://127.0.0.1:8000](http://127.0.0.1:8000)

You should see:

```json
{
  "message": "Hello Fatima! 🌸"
}
```

🎉 Congratulations! You've built your first API endpoint!

---

## Add More Routes (Pages)

Let’s add more pages to explore how routing works.

Update your `main.py` like this:

```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
def read_root():
    return {"message": "Hello Fatima! 🌸"}

@app.get("/about")
def about():
    return {"info": "This is your FastAPI journey!"}

@app.get("/user/{name}")
def get_user(name: str):
    return {"user": name}
```

Now try visiting:

- 👉 [http://127.0.0.1:8000/about](http://127.0.0.1:8000/about)
- 👉 [http://127.0.0.1:8000/user/Fatima](http://127.0.0.1:8000/user/Fatima)

You’ll see dynamic responses based on the URL!

---

## 📋 Automatic API Documentation 🎉

One of the best features of FastAPI is that it **automatically creates documentation** for your API.

Go to:

👉 [http://127.0.0.1:8000/docs](http://127.0.0.1:8000/docs)

You’ll see a beautiful UI where you can test all your routes by clicking buttons!

---

##  Test Without Postman

You don’t need Postman at all right now!  
Use the Swagger UI (`/docs`) to:

- See all available endpoints
- Try them out with real input
- View expected outputs

> Made by Dua Fatima
> Don't forget to follow my github.