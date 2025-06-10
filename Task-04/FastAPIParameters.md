

# FastAPI Parameters – Understanding Input Types

In this task, you'll learn how to get different kinds of inputs from users in FastAPI.  
This includes:

- Path parameters
- Query parameters
- Request body
- And how to combine them

Let’s go step by step.

---

## ✅ What Are Parameters?

**Parameters** are pieces of data that clients (like browsers or apps) send to your API.

There are different ways they can be sent:
- In the URL path
- After a question mark in the URL (query)
- Inside the request body as JSON

Each has its own use case.

---

## 🔹 1. Path Parameters – Get Data from the URL

Used when the value is part of the URL itself.

### Example:

```python
@app.get("/user/{user_id}")
def read_user(user_id: int):
    return {"user_id": user_id}
```

If you visit:

```
http://127.0.0.1:8000/user/123
```

You will get:

```json
{
  "user_id": 123
}
```

💡 Notes:
- `{user_id}` is a placeholder in the URL.
- The type (`int`) ensures only numbers are accepted.

---

## 🔹 2. Query Parameters – Optional Inputs in the URL

Used for optional filtering or settings, usually after a `?` in the URL.

### Example:

```python
@app.get("/items/")
def read_items(skip: int = 0, limit: int = 10):
    return {"skip": skip, "limit": limit}
```

If you visit:

```
http://127.0.0.1:8000/items/?skip=5&limit=20
```

You will get:

```json
{
  "skip": 5,
  "limit": 20
}
```

💡 Notes:
- These are optional because they have default values.
- Great for things like search filters or pagination.

---

## 🔹 3. Request Body – Send JSON Data in POST Requests

Used when you need to send more complex data, like user input forms.

### Step 1: Define a Pydantic Model

```python
from pydantic import BaseModel

class Item(BaseModel):
    name: str
    price: float
```

### Step 2: Use it in a POST Route

```python
@app.post("/items/")
def create_item(item: Item):
    return {"message": f"{item.name} costs {item.price}"}
```

If someone sends this JSON:

```json
{
  "name": "Book",
  "price": 499.99
}
```

You will get:

```json
{
  "message": "Book costs 499.99"
}
```

Notes:
- This uses Pydantic to validate the structure and types.
- Only valid JSON matching the model will be accepted.

---

## 🔹 4. Mix Path + Query + Body Together

You can use multiple types of parameters in one endpoint.

### Example:

```python
@app.put("/users/{user_id}")
def update_user(user_id: int, item: Item, active: bool = True):
    return {
        "id": user_id,
        "item": item,
        "active": active
    }
```

Here:
- `user_id` comes from the path
- `item` comes from the request body
- `active` is a query parameter

If you call:

```
PUT /users/10?active=false
Body: {"name": "Laptop", "price": 1200}
```

You’ll get:

```json
{
  "id": 10,
  "item": {
    "name": "Laptop",
    "price": 1200
  },
  "active": false
}
```

---

## 🔹 5. Required vs Optional Parameters

You can control whether a parameter is required or not.

### Example:

```python
@app.get("/products/")
def get_products(category: str = "all"):
    return {"category": category}
```

Here:
- `category` is optional
- If no value is given, it defaults to `"all"`

If you call:

```
GET /products/
```

You’ll get:

```json
{
  "category": "all"
}
```

---

| Parameter Type | How It Works | Example |
|----------------|--------------|---------|
| Path           | Part of the URL | `/user/123` |
| Query          | Optional values after `?` | `/search?limit=10` |
| Body           | JSON inside POST/PUT requests | `{"name": "Fatima"}` |
| Mixing         | You can use all together in one route | Yes! |
| Validation     | FastAPI checks types automatically | No manual checks needed |

---
> Made by Dua Fatima. don't forget to follow my GitHub.
