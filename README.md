# Research-Paper-Analyzer

# 📄 Agentic Research Paper Synthesizer

An autonomous, multi-agent workflow built with **LangGraph** and **LangChain** that dynamically extracts, evaluates, and structures data from complex academic PDFs. 

Unlike standard RAG (Retrieval-Augmented Generation) applications, this system utilizes an "Extractor-Critic" agentic loop. It evaluates its own extractions against user instructions and iteratively corrects its mistakes before returning the final JSON output, ensuring high-fidelity data extraction across any scientific domain.

## ✨ Key Features
* **Domain-Agnostic Extraction:** Pass in dynamic instructions at runtime to extract AI architectures, medical trial cohorts, or financial metrics without changing the underlying code.
* **Agentic Review Loop:** A built-in Critic Node validates the extracted data against the Pydantic schema and routes the workflow back to the Extractor if required data is missing.
* **Structured Output Validation:** Enforces strict JSON schemas using Pydantic, ensuring the output is ready for downstream database insertion or frontend display.
* **Automated PDF Parsing:** Seamlessly ingests and chunks multi-page academic PDFs.

## 🛠️ Tech Stack
* **Framework:** LangGraph, LangChain
* **LLM:** OpenAI (`gpt-4o-mini`)
* **Data Validation:** Pydantic
* **Document Processing:** PyPDFLoader

## 📂 Project Architecture

```text
research-paper-synthesizer/
├── src/
│   ├── state.py          # Defines Pydantic schemas and LangGraph state variables
│   ├── nodes.py          # Contains the Extractor and Critic LLM logic
│   ├── graph.py          # Wires the nodes into a cyclic state machine
│   └── document_utils.py # Handles PDF ingestion and text extraction
├── data/
│   └── raw_papers/       # Directory for target PDF files
├── main.py               # Orchestration engine and execution entry point
├── requirements.txt      # Project dependencies
└── .env                  # Environment variables (API Keys)


🚀 Getting Started
1. Clone the repository

git clone [https://github.com/nikoyasam/research-paper-synthesizer.git](https://github.com/nikoyasam/research-paper-synthesizer.git)
cd research-paper-synthesizer

2. Set up a virtual environment (Recommended)
python -m venv venv
# On Windows use: venv\Scripts\activate
# On macOS/Linux use: source venv/bin/activate

3. Install dependencies
pip install -r requirements.txt

4. Configure Environment Variables
Create a .env file in the root directory and add your OpenAI API key:
OPENAI_API_KEY=your_openai_api_key_here

5. Run the Pipeline
Place a research paper (e.g., sample_paper.pdf) into the data/raw_papers/ directory. Update the file path and specific extraction instructions in main.py, then run:
python main.py
