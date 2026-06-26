# Autonomous Multi-Agent Deep Research System

An enterprise-grade, multi-agent orchestration system that automates deep topical research, real-time web intelligence harvesting, and evidence-based synthesis. Built using a hierarchical state-machine architecture, the system coordinates specialized AI agents to crawl, validate, audit, and compile comprehensive, citation-backed intelligence reports with zero human intervention.

<img width="1408" height="768" alt="agent" src="https://github.com/user-attachments/assets/9eb406a1-08f7-420a-9a1c-93e82d48b736" />

## 🚀 Key Features & Architectural Highlights

- **Hierarchical Agent Coordination**: Implements a Supervisor-Worker topology to dynamically decompose complex research queries into parallelizable sub-tasks.
- **Self-Correcting Critique Loop**: A dedicated Auditor/Reviewer Agent evaluates generated reports against factuality and structural constraints, automatically triggering sub-agents to fill information gaps.
- **Deterministic Tool Execution**: Custom-built integration with neural search engines (Tavily/Exa) and web scrapers with automatic retry mechanisms and rate-limit handling.
- **Strict Grounding & Automated Citation**: Enforces absolute data grounding to eliminate LLM hallucinations; every statement in the final report maps back to a validated URL footprint.
- **State Management & Resiliency**: Built on state machines to ensure conversation context tracking and graceful error recovery during long-horizon research tasks.

## 🛠️ Tech Stack & Ecosystem

- **Framework & Orchestration:** Python 3.11+, LangGraph / CrewAI (State Management)
- **Core LLM Engines:** OpenAI GPT-4o / Anthropic Claude 3.5 Sonnet / Groq (Llama 3)
- **Data Harvesting & Search:** Tavily API, BeautifulSoup4, Exa AI
- **Frontend / Interface:** Streamlit (Custom styled UI with real-time process logs)
- **DevOps & Infrastructure:** Docker, GitHub Actions (CI/CD)

## 📐 System Architecture

The core architecture leverages a State Graph to handle multi-agent message transitions and shared global memory:

```mermaid
graph TD
    A[User Research Query] --> B[Supervisor / Planner Agent]
    B -->|Decompose & Delegate| C[Web Search Agent]
    B -->|Decompose & Delegate| D[Document Scraping Agent]
    C --> E[Shared State/Memory]
    D --> E[Shared State/Memory]
    E --> F[Synthesizer / Writer Agent]
    F --> G[Auditor / Reviewer Agent]
    G -- Pass: Generate Report --> H[Final Markdown Report]
    G -- Fail: Missing Data / Hallucination --> B


⚙️ Setup & Installation
Prerequisites
Python 3.10 or 3.11

API Keys for OpenAI/Anthropic and Tavily Search

Local Deployment
Clone the Repository:

Bash
git clone [https://github.com/shreyakoranga80-hash/Multi-Agent-Research-System.git](https://github.com/shreyakoranga80-hash/Multi-Agent-Research-System.git)
cd Multi-Agent-Research-System
Configure Environment Variables:
Create a .env file in the root directory:

Code snippet
OPENAI_API_KEY=your_openai_api_key
TAVILY_API_KEY=your_tavily_api_key
LOG_LEVEL=INFO
Run via Docker (Recommended):

Bash
docker build -t research-system .
docker run -p 8501:8501 --env-file .env research-system
Alternative (Local Virtual Environment):

Bash
python -m venv .venv
source .venv/bin/activate  # On Windows use `.venv\Scripts\activate`
pip install -r requirements.txt
streamlit run src/ui/app.py


🧪 Testing & Production Validation
Run the test suite to validate agent state transitions and tool execution:


Bash
pytest tests/

---


