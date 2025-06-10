# What Is Function/Tool Calling?

In this task, you’ll learn what **function calling (or tool calling)** is and why it’s such a powerful feature in modern AI systems like **LLMs**, **AI agents**, and **chatbots**.

##  What Is Function Calling?

**Function calling** (also called **tool calling**) means allowing an AI model to use external tools or functions — just like how a human would call a calculator or search the web when they don’t know something.

It gives LLMs the ability to:
- Access real-time data
- Perform actions (like sending emails)
- Use APIs
- Run code
- Make decisions based on up-to-date information

---

##  Why Do We Need It?

Imagine you ask an AI:
> "What is the weather in New York today?"

An AI without function calling might say:
> "I can't check real-time weather."

But with function calling, it can:
1. Recognize that it needs current weather data
2. Call a weather API function
3. Get the result
4. Tell you the answer

That’s the power of **function calling**!

---

##  How Does It Work?

Here’s how it works in most AI systems:

### Step 1: Define the Tool
You write a function or API that does something useful.

Example:

```python
def get_weather(city):
    # Simulate getting weather data
    return f"The weather in {city} is sunny and 75°F."
```

### Step 2: Register the Tool with the Model
You tell the AI that this tool exists and what it does.

### Step 3: User Asks a Question
> "What is the weather in London?"

### Step 4: The AI Decides to Use the Tool
The AI understands it needs to use `get_weather("London")`.

### Step 5: The Tool Returns Data
The function returns:
> "The weather in London is sunny and 75°F."

### Step 6: AI Gives Final Answer
The AI says:
> "The weather in London is sunny and 75°F."

---

## Real-World Examples of Tools

| Tool Name | What It Does |
|----------|--------------|
| `search_web()` | Searches the internet for current info |
| `get_weather()` | Gets current weather |
| `run_code()` | Runs Python or other code |
| `send_email()` | Sends an email |
| `calculate()` | Performs math operations |
| `database_query()` | Gets data from a database |

---

## How Function Calling Powers AI Agents

**AI agents** are programs that act autonomously to achieve goals.

They rely heavily on function calling to do things like:

| Agent Goal | Tools Used |
|-----------|------------|
| Book a flight | Search flights, check prices, book tickets |
| Write a report | Search the web, summarize data, generate text |
| Code a website | Write HTML/CSS, test code, debug errors |
| Manage tasks | Add items to to-do list, send reminders |

Without tools, agents can only give theoretical answers.  
With tools, they can **take real action**.

---

## Example: A Simple Tool in Code

Here’s how you define a tool in JSON format for use with OpenAI or similar platforms:

```json
{
  "name": "get_weather",
  "description": "Get the current weather in a given city.",
  "parameters": {
    "type": "object",
    "properties": {
      "city": {"type": "string", "description": "Name of the city"}
    },
    "required": ["city"]
  }
}
```

This tells the AI:
- What the tool does
- What input it needs (`city`)
- What type of data to expect

---

## Types of Tools You Can Use

| Type | Description |
|------|-------------|
| Built-in Tools | Provided by the platform (e.g., OpenAI) |
| Custom Functions | Your own code functions |
| Third-party APIs | Like Google Search, Weather API, etc. |
| Code Interpreter | Allows running code directly |
| Web Browsing Tools | Lets the agent search the internet |

---

## Benefits of Function Calling

| Benefit | Description |
|--------|-------------|
| Real-time data access | Get up-to-date info instead of old knowledge |
| Automation | Let the AI perform actions without manual help |
| Flexibility | Add any tool you want to expand AI capabilities |
| Accuracy | Avoid guessing — use real data from trusted sources |
| Scalability | Build complex AI assistants that grow with more tools |

---

##  Summary

| Concept | Meaning |
|--------|---------|
| Function Calling | Letting an AI use external tools or functions |
| Tool | A function or API that the AI can call |
| AI Agent | Uses tools to perform real-world tasks |
| Purpose | Give AI the ability to take action, not just talk |
| Real Use Cases | Weather lookup, web search, code execution, email automation |

---

> Made by Dua Fatima. Don't forget to follow my GitHub.