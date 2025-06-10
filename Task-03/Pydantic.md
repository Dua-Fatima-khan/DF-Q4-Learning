

#  Pydantic in FastAPI – Understanding Data Validation

In this task, you will learn how to use **Pydantic** with **FastAPI** to manage and validate user input data effectively.

---

## What is Pydantic?

**Pydantic** is a Python library that helps you define the structure of your data. It makes sure that the data coming into your application has the correct format and types.

For example:
- A person's age should be a number.
- An email should have an `@` symbol.
- A boolean field should only be `True` or `False`.

---

##  Why Use Pydantic in FastAPI?

Here are some key reasons:

| Benefit | Description |
|--------|-------------|
| Automatic validation | Checks if the input matches the expected type and format |
| Cleaner code | Define data structures once and reuse them |
| Easier debugging | Gets rid of invalid data before it causes errors |

---

##  Creating a Pydantic Model

A **model** is like a template for your data.

### Example:

```python
from pydantic import BaseModel

class User(BaseModel):
    name: str
    age: int
    is_active: bool
```

This model expects:
- `name` to be a string
- `age` to be an integer
- `is_active` to be a boolean (`True` or `False`)

---

## Using the Model in FastAPI

You can use this model in your API endpoints to receive and validate JSON input from users.

### Example Code:

```python
from fastapi import FastAPI
from pydantic import BaseModel

app = FastAPI()

class User(BaseModel):
    name: str
    age: int
    is_active: bool

@app.post("/users/")
def create_user(user: User):
    return {"message": f"Hello {user.name}, you're {user.age} years old!"}
```

When someone sends data like this:

```json
{
  "name": "Fatima",
  "age": 22,
  "is_active": true
}
```

FastAPI will:
1. Check if the data matches the model
2. Convert it into a Python object you can work with

---

## Built-in Validation

If someone sends incorrect data, like:

```json
{
  "name": "Fatima",
  "age": "twenty-two",
  "is_active": true
}
```

FastAPI will respond with an error:

```json
{
  "detail": [
    {
      "loc": ["body", "age"],
      "msg": "value is not a valid integer",
      "type": "type_error.integer"
    }
  ]
}
```

You don’t need to write any extra code — Pydantic handles all this automatically.

---

##  Optional Fields and Default Values

You can make certain fields optional by using `Optional` and set default values.

### Example:

```python
from typing import Optional

class User(BaseModel):
    name: str
    age: Optional[int] = None
    is_active: bool = True
```

Now:
- `age` is optional and defaults to `None`
- `is_active` defaults to `True` if not provided

---

## Validating Email, Password, and More

You can also enforce stricter rules, like checking if a string is a valid email address or meets minimum length requirements.

### Example:

```python
from pydantic import BaseModel, EmailStr, constr

class RegisterUser(BaseModel):
    username: constr(min_length=3, max_length=20)
    email: EmailStr
    password: constr(min_length=8)
```

This ensures:
- Username must be between 3 and 20 characters
- Email must be in a valid format (like `example@example.com`)
- Password must be at least 8 characters long

---

- **Pydantic** helps you define what kind of data your app should accept.
- You create models using classes and type hints.
- FastAPI uses these models to **automatically validate** incoming data.
- If data is invalid, FastAPI returns a clear error message.
- You save time and reduce bugs by avoiding manual checks.


>Made by Dua Fatima. Don't forget to follow my GitHub.