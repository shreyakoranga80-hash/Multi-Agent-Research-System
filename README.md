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

### Phase 2: Add 3 "Engineering-Level" Enhancements
To prove to a hiring engineer that you didn't just copy a tutorial, implement these three industry-standard features into your codebase:

1. **Structured Logging & Cost Tracking:** Don't just use `print()`. Implement Python's `logging` module. Add a utility that tracks the number of tokens consumed per research run so you can show recruiters you understand the *production costs* of LLMs.
2. **Robust Exception Handling:** When a website blocks your scraper or an API times out, the system shouldn't crash. Wrap your tools in try-except blocks with **exponential backoff retries** (using libraries like `tenacity`).
3. **Add a Basic CI/CD Pipeline:** Add a `.github/workflows/main.yml` file. This tells recruiters that your project follows proper software engineering workflows. 
   *(Example GitHub Action content to drop into your repo):*
   ```yaml
   name: Python CI
   on: [push, pull_request]
   jobs:
     build:
       runs-on: ubuntu-latest
       steps:
       - uses: actions/checkout@v3
       - name: Set up Python
         uses: actions/setup-python@v4
         with: {python-version: '3.11'}
       - name: Install dependencies
         run: pip install -r requirements.txt
       - name: Run Tests
         run: pytest
