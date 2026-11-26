# ✈️ TravelEase – AI Travel Booking Assistant

An AI-powered travel booking assistant built using **Python, LangChain, Groq LLM, Pydantic, and Google Sheets**.

TravelEase helps customers explore holiday packages, check package prices, understand booking requirements, and submit booking enquiries through a conversational AI agent.

## 📌 Project Overview

TravelEase is designed to simplify the initial travel enquiry process.

Customers can interact with the AI assistant using natural language. The agent understands their requirements, uses Python tools to retrieve package information, validates booking details, calculates estimated package costs, and stores complete booking enquiries in Google Sheets.

## 🎯 Problem Statement

Customers often need to contact travel agencies manually to:
- Know available holiday packages.
- Check package prices.
- Understand advance booking requirements.
- Share their travel details.
- Submit booking enquiries.

TravelEase provides a conversational AI interface to make this initial enquiry process easier and faster.

## ✨ Features

- **AI-Powered Conversations:** Understands customer questions using a Groq-powered LLM.
- **Holiday Package Information:** Provides details about available destinations, durations, and prices.
- **Tool Calling:** Uses Python functions as tools to retrieve package prices and check booking notice requirements.
- **Structured Output:** Converts unstructured customer messages into structured booking records using Pydantic.
- **Booking Validation:** Checks required customer details and the minimum 48-hour advance booking policy.
- **Automatic Price Calculation:** Calculates the estimated total package price based on the number of travellers.
- **Google Sheets Integration:** Saves booking enquiries in Google Sheets.
- **Agent Trace Analysis:** Uses `pretty_print()` to inspect agent decisions, tool calls, and responses.

## 🌍 Available Holiday Packages

| Destination | Duration | Price per Person |
|---|---:|---:|
| Goa | 3 Days | ₹5,000 |
| Kerala | 4 Days | ₹8,000 |
| Manali | 5 Days | ₹12,000 |
| Jaipur | 3 Days | ₹6,000 |

**Pricing Formula:**

Total Package Price = Price Per Person × Number of Travellers

Example: Goa package for 3 travellers = ₹5,000 × 3 = ₹15,000.

## 🛠️ Technologies Used

| Technology | Purpose |
|---|---|
| Python | Core programming language |
| LangChain | Agent creation and tool integration |
| Groq | LLM inference |
| GPT-OSS-20B | Language model |
| Pydantic | Structured data validation |
| Google Colab | Development and execution environment |
| Google Sheets | Booking enquiry storage |
| gspread | Google Sheets integration |

## 🧠 Agent Architecture

The application follows an agent-based workflow:

1. Customer sends a natural language message.
2. The AI agent understands the customer's request.
3. The agent selects an appropriate tool when required.
4. Python tools retrieve package prices or check booking requirements.
5. Pydantic validates structured booking information.
6. The booking enquiry is saved to Google Sheets when all required details and policy checks are satisfied.
7. The agent generates a response for the customer.

## 🔧 Tools Implemented

### 1. `get_package_price()`

Retrieves the actual package price and duration for a selected destination.

### 2. `check_booking_notice()`

Checks whether the requested travel date satisfies the minimum 48-hour advance booking policy.

### 3. `log_booking_enquiry()`

Validates customer details, calculates the estimated package price, and saves the booking enquiry into Google Sheets.

## 📋 Structured Output with Pydantic

The project uses a Pydantic model named `BookingEnquiry` to extract customer information into a structured format.

Fields include:

- `customer_name`
- `destination`
- `travel_date`
- `travellers`

The model helps validate data types and restrict destinations to the available holiday packages.

The project also uses LangChain's `with_structured_output()` to test structured extraction from five customer messages.

## 📊 Google Sheets Integration

Booking enquiries are stored in a Google Sheet with the following columns:

- Customer Name
- Destination
- Travel Date
- Travellers
- Price Per Person
- Total Price
- Enquiry Status

This helps maintain customer enquiry records without manually copying details from conversations.

## 🧪 Testing and Experiments

The project includes practical experiments to understand agent behaviour:

- Tested structured extraction using five customer messages.
- Compared prompt responses using different prompt configurations.
- Experimented with different LLM temperature settings.
- Tested tool selection with meaningful and vague tool names and descriptions.
- Inspected agent execution traces using `pretty_print()`.
- Counted tool calls and model calls for an agent interaction.

## 🚀 Getting Started

### Prerequisites

- Python
- Google account
- Groq API key
- Google Colab

### 1. Clone the Repository

```bash
git clone https://github.com/YOUR_USERNAME/TravelEase-AI-Agent.git
cd TravelEase-AI-Agent
```

### 2. Install Dependencies

```bash
pip install -U langchain langchain-groq gspread pydantic
```

### 3. Configure Groq API Key

Add your Groq API key to Google Colab Secrets using the name:

```text
GROQ_API_KEY
```

The notebook retrieves the key securely using Colab's `userdata` module.

Never upload API keys or credentials to GitHub.

### 4. Run the Notebook

1. Open `AI_Agent.ipynb` in Google Colab.
2. Add your Groq API key to Colab Secrets.
3. Run the notebook cells in order.
4. Authorize Google account access when prompted.
5. Test the TravelEase assistant.
6. Open the generated Google Sheet to view saved enquiries.

## 💬 Example Interaction

**Customer:**

Hi! My name is Ravi. I want to visit Goa on 20 December 2026 with 2 travellers. Please check the package price and save my booking enquiry.

**TravelEase AI:**

The Goa package costs ₹5,000 per person. For 2 travellers, the estimated total is ₹10,000. Your enquiry can be recorded, subject to the travel team's availability verification.

## ⚠️ Important Note

TravelEase currently records booking enquiries, not confirmed reservations.

- Actual hotel, flight, and transport availability is not connected to external booking systems.
- All enquiries remain subject to travel-team verification.
- Saving an enquiry does not confirm a holiday booking.
- The 48-hour advance booking policy is checked before an enquiry is saved.

## 🔮 Future Enhancements

- Integrate real-time hotel and flight availability APIs.
- Add a customer booking status tracker.
- Build a web-based travel booking interface.
- Add multilingual voice-based conversations.
- Integrate payment gateways.
- Add email or WhatsApp booking notifications.

## 👩‍💻 Learning Outcomes

Through this project, I explored and implemented:

- LLM integration using Groq.
- Agent creation using LangChain.
- Python function calling and custom tools.
- Pydantic structured output and validation.
- Google Sheets integration using gspread.
- Prompt engineering and testing.
- Agent execution trace analysis.

---

**TravelEase – Making Travel Enquiries Simpler with AI.** ✈️
