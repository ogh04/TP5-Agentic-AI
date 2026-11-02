# Agentic AI – TP corrigé

Ce projet adapte le TP LangChain/LangGraph fourni en un notebook pédagogique restructuré et corrigé.

## Démarrage
1. Installer Python 3.11+.
2. `python -m venv .venv`
3. Activer le venv (Windows : `.venv\Scripts\Activate.ps1`; macOS/Linux : `source .venv/bin/activate`).
4. `python -m pip install -r requirements.txt`
5. Copier `.env.example` en `.env` et remplacer `OPENAI_API_KEY` par une **nouvelle** clé valide.
6. Ouvrir `AI_Agentic_Corrige.ipynb` dans Jupyter ou VS Code, sélectionner `.venv` et exécuter les cellules dans l'ordre.

## Remarques
- Clé Nvidia présente dans le fichier de départ **intentionnellement non réutilisée** : la révoquer.
- Les outils de météo / actualités / employés / email sont simulés.
- Tavily et PostgreSQL sont optionnels.
- La section LangGraph fonctionne sans API si exécutée isolément.
- Vérification syntaxique effectuée ; aucune exécution réelle de modèles externes n'a été réalisée.

# Agentic AI with LangChain, LangGraph & Ollama

A hands-on educational project exploring the fundamentals of **Agentic AI** using LangChain, LangGraph, and locally hosted large language models through Ollama.

This project is based on an academic practical assignment (TP5) and has been adapted to run primarily with open-source models, without requiring a paid OpenAI API.

## Project Overview

The notebook demonstrates how to build AI agents that can:

- Maintain conversation history and memory.
- Dynamically select models based on context.
- Call external tools to perform tasks.
- Search the web using Tavily.
- Retrieve information with RAG and FAISS.
- Handle tool execution errors.
- Generate structured outputs using Pydantic.
- Protect personal information with middleware.
- Request human approval before sensitive actions.
- Filter specific user inputs.
- Execute state-based workflows with LangGraph.

## Technologies Used

| Technology | Purpose |
|------------|---------|
| Python 3.12 | Programming language |
| LangChain | Agent creation and tool integration |
| LangGraph | State management and workflows |
| Ollama | Local LLM inference |
| Qwen2.5:3b | Primary language model |
| Qwen2.5:7b | Advanced language model |
| nomic-embed-text | Local text embeddings |
| FAISS | Vector similarity search |
| Tavily | Web search |
| PostgreSQL | Persistent conversation storage |
| Pydantic | Structured output validation |

## Project Structure

```text
agentic_tp/
├── AI_Agentic_Corrige.ipynb
├── README.md
├── requirements.txt
├── .env.example
└── .gitignore
```

Local-only files such as `.env`, `.venv/`, and downloaded Ollama models are not included in the repository.

## Installation

### 1. Clone the repository

```bash
git clone https://github.com/ogh04/TP5-Agentic-AI.git
cd TP5-Agentic-AI
```

### 2. Create a virtual environment

```bash
python -m venv .venv
```

Activate it on Windows PowerShell:

```powershell
.\.venv\Scripts\Activate.ps1
```

On macOS/Linux:

```bash
source .venv/bin/activate
```

### 3. Install dependencies

```bash
python -m pip install -r requirements.txt
```

Ensure the environment includes the Ollama and PostgreSQL integrations:

```bash
python -m pip install langchain-ollama langgraph-checkpoint-postgres "psycopg[binary]"
```

### 4. Install and configure Ollama

Download Ollama from https://ollama.com/

Pull the models:

```bash
ollama pull qwen2.5:3b
ollama pull qwen2.5:7b
ollama pull nomic-embed-text
```

The models run locally and do not require an OpenAI API key.

### 5. Configure environment variables

Copy `.env.example` to `.env`.

Configure optional services when needed:

```dotenv
TAVILY_API_KEY=your_tavily_api_key
POSTGRES_URI=postgresql://postgres:your_password@localhost:5432/agentic_tp
```

For PostgreSQL, create the `agentic_tp` database before running the persistence example.

Keep `.env` private and never commit credentials to GitHub.

### 6. Run the notebook

Open `AI_Agentic_Corrige.ipynb` in VS Code or Jupyter Notebook.

Select the Python interpreter from `.venv` and execute the cells in order.

Some examples require Tavily or PostgreSQL to be configured.

## Practical Experiments

| Experiment | Status |
|------------|--------|
| Basic AI Agent | Tested |
| Conversation History | Tested |
| Dynamic Model Selection | Tested |
| In-Memory Conversation State | Tested |
| PostgreSQL Checkpoint Storage | Tested |
| Tool Calling | Tested |
| Tavily Web Search | Tested |
| Tool Error Handling | Tested |
| Dynamic System Prompts | Included |
| Structured Output with Pydantic | Tested |
| Middleware Lifecycle Hooks | Tested |
| RAG Agent with FAISS | Tested |
| PII Redaction | Tested |
| Human-in-the-Loop Approval | Tested |
| Content Filtering | Tested |
| LangGraph StateGraph | Tested |

**Validation note:** PostgreSQL checkpoint storage was tested, but recovery after restarting the Python kernel was not verified.

## Agentic RAG Example

The RAG experiment combines:

1. **OllamaEmbeddings** to generate text vectors.
2. **FAISS** to index and retrieve relevant passages.
3. **LangChain Retriever Tool** to expose retrieval to the agent.
4. **Qwen2.5:7b** to select the retrieval tool and generate a response.

The experiment confirmed tool invocation, document retrieval, and response generation using retrieved information.

## Human-in-the-Loop Example

The notebook demonstrates how to pause agent execution before a sensitive tool action.

The user can review the proposed action and approve it before execution resumes.

The email example is simulated: **no real emails are sent**.

## Security Notes

- Never commit `.env` or credentials.
- Review notebook outputs before publishing.
- Demo weather, news, employee, and email tools return simulated data.
- API-based search requires an active Tavily API key.
- PII redaction and content filtering are educational examples, not complete security solutions.

## Learning Outcomes

This project provides practical experience with the core building blocks of Agentic AI, including tool use, memory, retrieval, middleware, structured outputs, and graph-based workflows.

It is intended as an educational foundation for developing more advanced AI agent applications.

## Author

**Omar GHILAN**

- GitHub: https://github.com/ogh04
- LinkedIn: https://www.linkedin.com/in/omarghilan/

## License

This repository contains educational material adapted from an academic practical assignment. Reuse and redistribution should respect the original material's permissions.
