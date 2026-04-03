# 📄 Agentic Research Paper Synthesizer (Local AI Edition)

An autonomous, multi-agent workflow built with **LangGraph** and **LangChain** that dynamically extracts, evaluates, and structures data from complex academic PDFs. 

Unlike standard RAG (Retrieval-Augmented Generation) applications, this system utilizes an "Extractor-Critic" agentic loop. It evaluates its own extractions against user instructions and iteratively corrects its mistakes before returning the final JSON output. 

**This project is configured to run 100% locally and offline using Ollama, ensuring zero API costs and complete data privacy for sensitive academic or corporate documents.**

## ✨ Key Features
* **Domain-Agnostic Extraction:** Pass in dynamic instructions at runtime to extract methodologies, architectures, or evaluation metrics without changing the underlying code.
* **Agentic Review Loop:** A built-in Critic Node validates the extracted data against the Pydantic schema and routes the workflow back to the Extractor if required data is missing.
* **Structured Output Validation:** Enforces strict JSON schemas using Pydantic, ensuring the output is ready for downstream database insertion or frontend display.
* **Local & Secure Inference:** Uses Meta's Llama 3.1 running locally via Ollama, removing reliance on paid APIs and preventing proprietary data leaks.



## 📂 Project Architecture

```text
paper_reviewer/
├── requirements.txt      # List of libraries to install (pip install -r requirements.txt)
├── main.py               # The script you run in the terminal to start the whole app
├── src/                  # This folder holds all the puzzle pieces
│   ├── __init__.py       # Empty file (tells Python this is a module)
│   ├── state.py          # Defines the Pydantic models (UniversalPaperExtraction, AgentState)
│   ├── nodes.py          # BOTH extraction_node() and critic_node() live in here!
│   ├── graph.py          # Wires the nodes together into a loop (build_graph)
│   └── document_utils.py # Contains the load_and_parse_pdf() function
└── data/
    └── raw_papers/       # Drop your downloaded PDF files in here

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

