# 🤖 AI Agents & Automation Portfolio

Welcome to my portfolio of AI-powered automation workflows and intelligent agents built with **[n8n](https://n8n.io/)**. 

This repository showcases my ability to integrate LLMs, databases, APIs, and business tools to solve real-world problems through advanced process automation.

---

## 🚀 Projects Included

### 1. [AI Workflow Automation System (`n8n-ai-automation-system`)](./n8n-ai-automation-system/)
A complete customer service and data processing pipeline built for a real estate business. It handles incoming WhatsApp messages and delegates them to specialized AI agents.

**Key Features:**
- **LLM Supervisor (Router):** Analyzes intent and routes user queries to the appropriate agent (RAG, Classifier, or General Greeting).
- **RAG Agent (Retrieval-Augmented Generation):** Uses vector embeddings (Pinecone/Supabase) to answer complex inquiries based on PDF documents.
- **Support & Complaints Classifier:** Detects negative sentiment, urgency, and escalates complaints to human support.
- **Analytics Dashboard Integration:** Records all interactions and token usage costs to a Supabase database, updating a live Google Sheets dashboard.
- **Automated Cost Tracking:** Dynamically calculates API costs depending on the LLM model used.

**Technologies Used:**
- **n8n** for visual workflow orchestration.
- **LLMs:** Meta LLaMA 3.1, Google Gemini 2.5 Flash, OpenAI Text Embeddings.
- **Integrations:** WhatsApp Business API, Supabase (PostgreSQL), Google Sheets, Pinecone.

**Architecture Overview:**

![Workflow Architecture](./n8n-ai-automation-system/screenshots/workflow-overview.jpg)

---

## 🛠️ Skills & Tools

- **Workflow Orchestration:** n8n, Make, Zapier.
- **AI & Machine Learning:** LangChain, RAG architectures, Prompt Engineering, Agentic AI systems.
- **APIs & Integrations:** RESTful APIs, Webhooks, OAuth2.
- **Databases:** PostgreSQL, Supabase, Vector Databases (Pinecone, Qdrant).
- **Languages:** JavaScript / Node.js (for custom n8n code nodes), Python.

---

## 📥 How to use these workflows

1. Clone this repository:
   ```bash
   git clone https://github.com/sergioRancibia/n8n-automation-ai-agents-portfolio.git
   ```
2. Open your local or self-hosted n8n instance.
3. Import the `.json` files found in the `workflows/` directories.
4. **Important:** All sensitive credentials, API keys, and Webhooks have been sanitized for security. You will need to reconfigure the `Credentials` inside n8n with your own API keys (e.g., Supabase, Groq, Gemini, WhatsApp).

---

*Feel free to explore the code nodes and workflow architectures. If you have any questions or want to discuss automation opportunities, please reach out!*
