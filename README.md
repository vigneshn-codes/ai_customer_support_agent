# AI Customer Support Agent with Memory

A simple web app that acts as a **customer support chatbot** for an electronics store (TechGadgets.com). The bot **remembers** past conversations per customer, so it can answer follow-up questions about orders and history.

---

## What it does

- You chat with an AI support agent as if you were a customer.
- The agent remembers what was said before (per customer ID).
- You can generate fake customer data (orders, profile) to try the bot with realistic context.
- You can view stored “memories” for any customer.

---

## What you need

1. **Python 3.10+**
2. **OpenAI API key** – [Create one here](https://platform.openai.com/account/api-keys). The key must start with `sk-` or `sk-proj-`.
3. **Qdrant** – A small database that stores the agent’s memory. It must be running on your machine (see below).

---

## Install and run

### 1. Clone or open the project folder

```bash
cd ai_customer_support_agent
```

### 2. Create a virtual environment and install dependencies

```bash
python -m venv myenv
source myenv/bin/activate   # On Windows: myenv\Scripts\activate
pip install -r requirements.txt
```

### 3. Run Qdrant (for memory storage)

The app expects Qdrant at **localhost:6333**. Easiest way is with Docker:

```bash
docker run -p 6333:6333 qdrant/qdrant
```

If you don’t use Docker, install and run Qdrant by following [Qdrant’s docs](https://qdrant.tech/documentation/quick-start/).

### 4. Start the app

```bash
streamlit run customer_support_agent.py
```

Your browser will open the app (usually at http://localhost:8501).

---

## How to use the app

1. **Enter your OpenAI API key**  
   Paste your key in the box (starts with `sk-` or `sk-proj-`). The app will tell you if the format looks wrong.

2. **Enter a Customer ID** (in the sidebar)  
   Any string is fine, e.g. `customer_001`. The agent keeps separate memories per ID.

3. **(Optional) Generate synthetic data**  
   Click **“Generate Synthetic Data”** to create fake orders and profile for that customer. The agent will use this when you chat.

4. **Chat**  
   Type in the chat box. The agent answers using past context and (if you generated it) the synthetic customer data.

5. **(Optional) View memory**  
   Click **“View Memory Info”** in the sidebar to see what the agent has stored for that customer.  
   Click **“View Customer Profile”** to see the generated profile in JSON.

---

## Project structure

| File | Purpose |
|------|--------|
| `customer_support_agent.py` | Main app (Streamlit UI + support agent logic) |
| `requirements.txt` | Python dependencies (Streamlit, OpenAI, Mem0) |
| `pyrightconfig.json` | IDE/linter config (points to `myenv`) |

---

## Troubleshooting

- **“Incorrect API key”** – Use a valid key from [OpenAI API keys](https://platform.openai.com/account/api-keys). Keys start with `sk-` or `sk-proj-` and are long.
- **“Failed to initialize memory”** – Start Qdrant so it’s reachable at `localhost:6333`.
- **Import errors in the IDE** – Ensure the IDE’s Python interpreter is set to the project’s `myenv` (or that `pyrightconfig.json` is in the project root).
