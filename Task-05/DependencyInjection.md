# Understanding Dependency Injection in FastAPI

In this task, you’ll learn how to use **Dependency Injection (DI)** in FastAPI.  
This is a way to reuse code across different parts of your application — especially useful for things like:

- User authentication
- Database connections
- App settings
- Reusable logic

Let’s break it down step by step.

---

##  What Is Dependency Injection?

**Dependency Injection (DI)** means:

> Instead of writing the same code again and again inside each route, you write it once and "inject" it where needed.

Think of it like:
- Writing a helper function that does something important
- Then using it in multiple places without repeating yourself

---

## 🔹 1. Basic Example – Injecting a Function

```python
from fastapi import Depends, FastAPI

app = FastAPI()

def get_token():
    return "secret-token-123"

@app.get("/items/")
def read_items(token: str = Depends(get_token)):
    return {"token_used": token}
```

### How It Works:
- `get_token()` returns a value
- The `/items/` route uses `Depends(get_token)` to access that value
- You don’t have to call `get_token()` manually

Output when you visit `/items/`:

```json
{
  "token_used": "secret-token-123"
}
```

---

## 🔹 2. Real Use Case – Get Current User

You can inject functions that check if a user is logged in.

```python
from fastapi import HTTPException

def get_current_user():
    # Simulate a logged-in user
    user = {"username": "Fatima"}
    if not user:
        raise HTTPException(status_code=401, detail="Not logged in")
    return user

@app.get("/profile")
def read_profile(current_user: dict = Depends(get_current_user)):
    return {"user": current_user}
```

### What This Does:
- Checks if there is a logged-in user
- If not, returns an error (401 Unauthorized)
- If yes, gives the user data to the route

---

## 🔹 3. Using Classes as Dependencies

You can also inject classes — great for managing configuration or services.

```python
class Settings:
    def __init__(self):
        self.db_url = "mysql://localhost"

def get_settings():
    return Settings()

@app.get("/config")
def config(settings: Settings = Depends(get_settings)):
    return {"db": settings.db_url}
```

### Why Use Classes?
- Helps organize complex logic
- Easy to test and change later
- Keeps your app flexible and clean

---

## 🔹 4. Nested Dependencies – Dependencies Inside Dependencies

Sometimes one dependency needs another.

```python
def db_connection():
    return "Fake DB Connection"

def get_user(db=Depends(db_connection)):
    return f"User from {db}"

@app.get("/nested")
def nested(user=Depends(get_user)):
    return {"user": user}
```

### Output when visiting `/nested`:

```json
{
  "user": "User from Fake DB Connection"
}
```

This is super helpful when building large apps with many layers of logic.

---


| Concept | Description |
|--------|-------------|
| `Depends()` | Tells FastAPI to run a function before calling the route |
| Reusability | Use the same logic in multiple routes |
| Clean Code | Routes stay short and focused on their main job |
| Common Uses | Authentication, database setup, app settings, permission checks |

---

> Made by Dua Fatima. Don't forget to follow GitHub.