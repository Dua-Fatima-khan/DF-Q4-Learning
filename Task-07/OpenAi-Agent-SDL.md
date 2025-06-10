
# Introduction to the OpenAI Agent SDK

In this task, you'll learn how to use the **OpenAI Agent SDK** to create your own **AI-powered agent** — a smart program that can perform tasks using tools and reasoning.

This is a powerful concept used in modern AI systems like AutoGPT, BabyAGI, and more.

---

##  What Is the OpenAI Agent SDK?

The **OpenAI Agent SDK** allows you to build **AI assistants** that can:

- Understand natural language instructions
- Use tools (like APIs, code execution, search engines)
- Make decisions based on goals
- Solve complex problems step-by-step

These are called **agents** because they act autonomously to complete tasks.

---

##  Real-World Use Cases

Here are some examples of what you can build with an AI agent:

| Use Case | Description |
|----------|-------------|
| Research Assistant | Ask a question and have the agent find and summarize information from the web |
| Code Generator | Ask the agent to write code, and it uses a Python interpreter tool |
| Email Automation | Have the agent check emails and take actions based on content |
| Data Analyst | Upload a CSV file and ask the agent to analyze and visualize data |

---

##  How Does an AI Agent Work?

An agent follows this basic structure:

1. **Goal**: You give it a task.
2. **LLM (Large Language Model)**: It uses GPT-4 or another model to reason and plan.
3. **Tools**: The agent selects and uses functions or APIs to get real-world data.
4. **Loop**: It keeps thinking and using tools until the goal is achieved.

Think of it as a robot brain that thinks, decides, and acts.

---

##  Step-by-Step Example Using the SDK

Let’s walk through a simple example where the agent adds two numbers using a custom function.

### 1. Install Required Package

First, install the OpenAI SDK:

```bash
pip install openai
```

### 2. Import Libraries and Set Up API Key

```python
from openai import OpenAI
import os

client = OpenAI(api_key=os.getenv("OPENAI_API_KEY"))
```

> Make sure to set your OpenAI API key in the environment variables.

### 3. Define a Tool (Function)

Create a simple function that will be used by the agent:

```python
def add_numbers(a, b):
    return a + b
```

Then, define this function in a format that OpenAI understands:

```python
tool = {
    "type": "function",
    "function": {
        "name": "add_numbers",
        "description": "Add two numbers together.",
        "parameters": {
            "type": "object",
            "properties": {
                "a": {"type": "integer"},
                "b": {"type": "integer"}
            },
            "required": ["a", "b"]
        }
    }
}
```

### 4. Create an Assistant (Your Agent)

Now, create the assistant using the OpenAI API:

```python
assistant = client.beta.assistants.create(
    name="Math Helper",
    instructions="You can add numbers using the add_numbers tool.",
    tools=[tool],
    model="gpt-4"
)
```

### 5. Start a Thread

A thread holds the conversation history between the user and the assistant:

```python
thread = client.beta.threads.create()
```

### 6. Send a Message to the Assistant

Ask the assistant a question:

```python
client.beta.threads.messages.create(
    thread_id=thread.id,
    role="user",
    content="What is 4 + 9?"
)
```

### 7. Run the Assistant

Start the assistant to process the message:

```python
run = client.beta.threads.runs.create(
    assistant_id=assistant.id,
    thread_id=thread.id
)
```

> In a real application, you would now monitor the run status and retrieve the response once it's completed.

---

##  What You Need to Use the SDK

| Requirement | Description |
|------------|-------------|
| OpenAI Account | Sign up at [https://platform.openai.com/](https://platform.openai.com/) |
| API Key | Found under your account settings |
| GPT-4 Access | Some features may require approval |
| Tools | Functions or APIs the agent can call |
| Threads | Conversations between user and agent |
| Runs | Each time the agent processes a request |

---

## Ideas for Projects

Here are some project ideas you can try:

| Project Idea | What the Agent Can Do |
|--------------|------------------------|
| Personal Researcher | Search the web and summarize findings |
| Code Helper | Write and test Python code |
| PDF Reader | Analyze uploaded PDF files and answer questions |
| Task Scheduler | Manage your daily tasks and reminders |

---

##  Optional Tools & Integrations

As you grow, you can integrate the OpenAI Agent SDK with:

- LangChain tools
- Browser automation tools
- File management tools
- Math and code interpreters

---


| Concept | Description |
|--------|-------------|
| Agent | An AI assistant that performs tasks |
| Tool | A function or API the agent can use |
| Thread | A conversation between user and agent |
| Run | A single execution of a task |
| SDK | Software Development Kit for building agents |

---

> Made by Dua Fatima. Don't forget to follow my GitHub.