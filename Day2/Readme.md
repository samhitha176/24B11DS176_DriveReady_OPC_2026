# 🍰 Sweet Crumbs Home Bakery – AI Chatbot with Memory

## 1. Project Overview

Sweet Crumbs Home Bakery is an AI-powered chatbot developed using Python and Groq LLM API.

The chatbot acts as a virtual bakery assistant. It can interact with customers, answer menu-related questions, remember customer details, and provide information about their orders.

This project is part of my **Agentic AI Learning Journey – Day 2: Prompts, Memory and Python Agents.**

---

## 2. Technologies Used

| Technology | Purpose |
|---|---|
| Python | Main programming language |
| Groq API | Connects the application to an LLM |
| OpenAI SDK | Communicates with the Groq API |
| Google Colab | Development environment |
| JSON | Stores and formats structured information |

---

## 3. Code Explanation

### Step 1: Import Required Libraries

```python
import json
import functools

from openai import (
    OpenAI,
    RateLimitError,
    APIConnectionError,
    AuthenticationError
)
from google.colab import userdata
```

**Explanation:**

- `json`: Converts Python data into JSON format.
- `functools`: Provides utilities for working with decorators.
- `OpenAI`: Creates an API client to communicate with Groq.
- `RateLimitError`: Handles API request limit errors.
- `APIConnectionError`: Handles connection problems.
- `AuthenticationError`: Handles invalid API key errors.
- `userdata`: Accesses secrets stored in Google Colab.

### Step 2: Configure the AI Model

```python
MODEL = "openai/gpt-oss-20b"
```

**Explanation:**

Here, we specify the LLM model that powers our chatbot.

- `MODEL` stores the model name.
- The chatbot sends customer messages to this model.
- The model generates responses based on the input and conversation context.

### Step 3: Create a Bakery Menu Using a Dictionary

```python
MENU = {
    "plum cake": 500,
    "chocolate cake": 650,
    "cupcake": 80
}
```

**Explanation:**

A Python dictionary stores bakery items and their prices.

- Keys represent cake names.
- Values represent their prices in Indian Rupees.

For example:

`MENU["chocolate cake"]` returns `650`.

Using a dictionary makes it easier to maintain and retrieve menu information.

### Step 4: Create a System Prompt

```python
SYSTEM = f"""
ROLE: You are the friendly assistant for Sweet Crumbs Home Bakery.

FACTS:
Menu with prices in rupees: {json.dumps(MENU)}
Orders need 24 hours' notice.
All cakes have eggless versions.

RULES:
Never promise a delivery time.
If it isn't in FACTS, say "I'll check with the owner."
Remember the customer's name and order during the chat.

FORMAT:
Under 50 words, friendly, English or Telugu
matching the customer.
"""
```

**Explanation:**

A system prompt defines how the AI assistant should behave.

It contains four important sections:

**1. ROLE:** Defines the chatbot's identity as a bakery assistant.

**2. FACTS:** Provides accurate bakery information, including menu prices and order requirements.

**3. RULES:** Sets boundaries to prevent the chatbot from making unsupported promises.

**4. FORMAT:** Controls the response length, tone, and language.

`json.dumps(MENU)` converts the Python menu dictionary into JSON-formatted text so the model can understand the menu information.

### Step 5: Decorators

A decorator is a Python function that adds extra functionality to another function without changing its original code.

```python
def my_decorator(func):
    @functools.wraps(func)
    def wrapper(*args, **kwargs):
        print("Before function execution")
        result = func(*args, **kwargs)
        print("After function execution")
        return result
    return wrapper
```

**Explanation:**

- `my_decorator()` receives another function.
- `wrapper()` executes additional instructions.
- `func(*args, **kwargs)` calls the original function.
- `functools.wraps()` preserves the original function's metadata.

Decorators help add reusable functionality such as logging, timing, and error handling.

### Step 6: Chatbot Memory

The chatbot maintains conversation history using a list of messages.

```python
messages = [
    {"role": "system", "content": SYSTEM}
]
```

**Explanation:**

Each message has two important fields:

- `role`: Identifies who is speaking.
- `content`: Contains the actual message.

Common roles:

| Role | Meaning |
|---|---|
| system | Defines chatbot behaviour |
| user | Customer's message |
| assistant | Chatbot's response |

When a customer shares their name or order details, previous messages remain available in the conversation history.

This allows the chatbot to answer questions based on earlier conversations.

### Step 7: Conversation History Trimming

```python
MAX_TURNS = 8
```

**Explanation:**

Conversation history can become very long.

To control its size, we retain only the latest messages.

This helps:
- Reduce unnecessary token usage.
- Manage conversation context.
- Avoid sending excessive conversation history.

**Important:** If the implementation slices the last eight messages, it retains eight messages, not eight complete user-assistant turns. The system prompt should also be preserved separately.

### Step 8: Groq API Integration

```python
client = OpenAI(
    api_key=userdata.get("GROQ_API_KEY"),
    base_url="https://api.groq.com/openai/v1"
)
```

**Explanation:**

This creates a connection between our Python application and Groq.

- `api_key`: Retrieves the secret API key from Google Colab.
- `base_url`: Specifies the Groq API endpoint.
- `OpenAI()`: Uses the OpenAI-compatible SDK to communicate with Groq.

The API allows our chatbot to send messages to the LLM and receive AI-generated responses.

### Step 9: Exception Handling

```python
try:
    # API request
    pass

except RateLimitError:
    print("API rate limit reached.")

except AuthenticationError:
    print("Invalid API key.")

except APIConnectionError:
    print("Connection problem.")

except Exception as e:
    print("Something went wrong:", e)
```

**Explanation:**

Exception handling prevents the application from stopping unexpectedly when an error occurs.

- `try`: Executes the code that may cause an error.
- `except RateLimitError`: Handles request limit errors.
- `except AuthenticationError`: Handles authentication failures.
- `except APIConnectionError`: Handles network connection failures.
- `except Exception`: Handles other unexpected errors.

---

## 4. How the Chatbot Works

The overall workflow:

1. Customer enters a message.
2. Python adds the message to conversation history.
3. The system prompt provides instructions to the AI.
4. The application sends the conversation to Groq.
5. The LLM generates a response.
6. The chatbot displays the response.
7. The conversation history is updated for future messages.

## 5. Sample Output

**Customer:** Hi, my name is Ravi.

**Chatbot:** Nice to meet you, Ravi!

**Customer:** I need two chocolate cakes.

**Chatbot:** Two chocolate cakes cost ₹1,300.

**Customer:** What is my name?

**Chatbot:** Your name is Ravi!

**Customer:** What did I order?

**Chatbot:** You ordered two chocolate cakes!

*Illustrative responses; actual model output may vary.*

## 6. Additional Practice Tasks

- Remove system prompt rules and compare chatbot behaviour.
- Build a classifier using few-shot prompting.
- Extract customer details into structured JSON.
- Change the conversation history limit and observe memory behaviour.
- Create a custom business menu and system prompt.

## 7. Key Learnings

By completing this project, I learned:

- How system prompts control LLM behaviour.
- How different message roles work.
- How Python dictionaries store business information.
- How decorators add reusable functionality.
- How conversation history enables contextual responses.
- How to integrate LLMs using APIs.
- How to handle API errors using exceptions.

---

**Day 2 Completed – Prompts, Memory and Python Agents 🚀**

Continuing my hands-on journey into Agentic AI, one concept and one project at a time.
