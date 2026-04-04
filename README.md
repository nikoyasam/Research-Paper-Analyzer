# 📄 Agentic Research Paper Synthesizer (Gemini Edition)

An autonomous, multi-agent workflow built with **LangGraph** and **LangChain** that dynamically extracts, evaluates, and structures data from complex academic PDFs. 

Unlike standard RAG (Retrieval-Augmented Generation) applications, this system utilizes an "Extractor-Critic" agentic loop. It evaluates its own extractions against user instructions and iteratively corrects its mistakes before returning the final JSON output. 

**This project leverages Google Gemini's massive 1-Million Token context window, allowing the system to ingest and analyze entire, un-chunked research papers in a single pass without losing critical context.**

## ✨ Key Features
* **Massive Context Ingestion:** Processes entire academic papers simultaneously without relying on complex chunking or vector databases, preserving the relationship between early methodologies and final conclusions.
* **Domain-Agnostic Extraction:** Pass in dynamic instructions at runtime to extract methodologies, deep learning architectures, or evaluation metrics (like EER) without changing the underlying code.
* **Agentic Review Loop:** A built-in Critic Node validates the extracted data deterministically and routes the workflow back to the Extractor if required data is missing.
* **Structured Output Validation:** Enforces strict JSON schemas using Pydantic, ensuring the output is ready for downstream database insertion or frontend display.

## 🛠️ Tech Stack
* **Framework:** LangGraph, LangChain
* **LLM Engine:** Google Gemini (`gemini-flash-latest`)
* **Data Validation:** Pydantic
* **Document Processing:** PyPDFLoader

## 📂 Project Architecture

```text
paper_reviewer/
├── requirements.txt      # List of project dependencies
├── main.py               # Orchestration engine and execution entry point
├── src/                  # Core logic and modules
│   ├── __init__.py       
│   ├── state.py          # Defines Pydantic schemas and LangGraph state variables
│   ├── nodes.py          # Contains the Extractor and Critic LLM logic
│   ├── graph.py          # Wires the nodes into a cyclic state machine
│   └── document_utils.py # Handles PDF ingestion and text extraction
└── data/
    └── raw_papers/       # Directory for target PDF files

## 🚀 Getting Started

```bash
# 1. Clone the Repository
git clone https://github.com/nikoyasam/research-paper-synthesizer.git
cd research-paper-synthesizer

# 2. Set Up a Virtual Environment (Recommended)
# Create virtual environment
python -m venv venv

# Activate environment
# Windows
venv\Scripts\activate
# macOS/Linux
source venv/bin/activate

# 3. Install Dependencies
pip install -r requirements.txt

# 4. Install and Run Ollama
# Pull Llama 3.1 model
ollama pull llama3.1

# Start the Ollama server
ollama serve

# 5. Run the Pipeline
python main.py

