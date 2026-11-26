# TravelEase – Smart Travel Booking Assistant

## Day 3: Your First Agent with LangChain

TravelEase is a fictional travel agency used to practise building an AI-powered customer support assistant with **LangChain** and **Groq**.

The assistant answers questions about holiday packages, prices, booking requirements, and basic travel FAQs. It also keeps track of the conversation history so it can remember details shared by the customer.

> **Note:** TravelEase is a learning project. It does not connect to real booking systems and cannot verify live hotel, flight, transport, or package availability. It must never claim that a booking is confirmed.

## Business details

| Destination | Duration | Price per person |
|---|---:|---:|
| Goa | 3 days | ₹5,000 |
| Kerala | 4 days | ₹8,000 |
| Manali | 5 days | ₹12,000 |
| Jaipur | 3 days | ₹6,000 |

### Booking rules

- Package prices are per person.
- A booking enquiry should be made at least 48 hours before travel.
- The assistant can collect the customer's name, destination, travel date, and number of travellers.
- The assistant must not confirm a booking without actual verification.
- The assistant must not invent hotel, flight, or transport availability.
- If information is unavailable, it should say: **"I'll check with our travel team."**
- Total package price = price per person × number of travellers.

## Technologies used

- Python
- Google Colab
- LangChain
- langchain-groq
- Groq LLM
- CSV for test cases

## Project features

1. **Business-specific system prompt** – defines the assistant's role, package information, booking rules, and response style.
2. **LangChain prompt template** – combines the system prompt, conversation history, and the customer's latest question.
3. **Conversation memory** – passes earlier messages to the model so it can remember details during the conversation.
4. **Customer-question tests** – checks whether responses include expected keywords from `tests.csv`.
5. **Prompt improvement experiment** – adds stricter pricing and booking instructions and compares the test scores.
6. **Temperature experiment** – runs the tests with temperature set to `1.0` twice to observe response variation.
7. **LangChain agent preview** – creates an agent with an empty tool list as an introduction to the agent interface.
8. **Day 4 preparation** – defines Python functions for package-price lookup and checking the 48-hour booking notice.

## Setup and execution

### 1. Open the notebook

Open the Day 3 TravelEase notebook in Google Colab.

### 2. Add your Groq API key to Colab Secrets

In Google Colab:

1. Open the **Secrets** panel.
2. Add a secret named `GROQ_API_KEY`.
3. Paste your Groq API key as its value.
4. Enable notebook access to the secret.

Do not paste your API key directly into the notebook or upload it to GitHub.

### 3. Run the notebook cells in order

The notebook installs the required libraries, reads the key from Colab Secrets, initializes the Groq chat model, and builds the TravelEase assistant.

The model used in the Day 3 tutorial is `openai/gpt-oss-20b`. If this model is unavailable to your Groq account, use a model currently supported by your Groq account.

## Test cases

The notebook creates a `tests.csv` file containing 10 customer questions and the expected keyword for each question.

Example:

| Customer question | Expected keyword |
|---|---|
| What is the price of the Goa package? | `5000` |
| How much is the Kerala package? | `8000` |
| Tell me the price of Manali package. | `12000` |
| What is the Jaipur package price? | `6000` |
| How much will two people pay for Goa? | `10000` |

The test runner sends each question to the chain and checks whether the expected keyword appears in the response. It prints the number of passed tests and the pass percentage.

**Important:** These are simple keyword-based checks, not a complete evaluation of answer quality. Model responses can vary, so inspect failed answers and improve the prompt where necessary. Do not report a pass rate until you have actually run the notebook.

## Experiments

### Prompt improvement

The second prompt version adds clearer instructions to:
- Multiply the per-person package price by the number of travellers.
- State the total price when the number of travellers is provided.
- Explain the 48-hour minimum notice for bookings.
- Avoid claiming that a booking is confirmed without verification.

Run the tests before and after the change and compare the scores.

### Temperature

The notebook creates another model instance with `temperature=1.0` and runs the tests twice. Compare the answers and pass rates to see whether the responses vary.

## Agent or not?

| Business task | Suitable approach |
|---|---|
| Calculate a package price | Plain Python code |
| Generate a travel advertisement | One LLM call |
| Check package details, verify booking requirements, and handle a booking enquiry through connected systems | Agent |

Use the simplest approach that can safely complete the task. An agent becomes useful when it needs to decide which actions or tools to use to reach a goal.

## Python functions prepared for Day 4

### `get_package_price(destination: str) -> int | None`

Returns the listed price per person for a destination, or `None` if the destination is not in the package list.

### `check_booking_notice(hours_before_travel: int) -> bool`

Returns `True` when the booking meets the minimum 48-hour notice and `False` otherwise.

These functions are currently standalone Python functions. They are not connected as agent tools in the Day 3 preview.

## Important limitation

The Day 3 agent preview uses `tools=[]`. It demonstrates the LangChain agent interface, but it cannot perform real bookings, check live availability, or save customer enquiries. Connecting safe, verified tools is a later step.

## Learning outcomes

By completing this project, I practised:

- Creating a business-specific system prompt.
- Using LangChain's `ChatPromptTemplate`.
- Adding conversation history with `MessagesPlaceholder`.
- Building a chain with the pipe operator (`|`).
- Parsing model output with `StrOutputParser`.
- Testing responses using a CSV file.
- Comparing prompt versions and temperature settings.
- Creating a basic LangChain agent preview.
- Writing typed Python functions in preparation for agent tools.

## Next step

**Day 4:** Connect Python functions as tools so the TravelEase agent can look up package prices and check booking requirements before responding.
