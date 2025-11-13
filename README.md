# RAG on Apple 10-K

A small Retrieval-Augmented Generation (RAG) project that answers questions from Apple’s official 10-K financial report using FAISS and a local LLM (Ollama).

## 🧠 Project Overview

This project was part of my Master’s program in Artificial Intelligence.
The goal was to build a simple system that can read a company’s 10-K report from the U.S. Securities and Exchange Commission (SEC) and answer natural language questions about it.

I chose Apple Inc. for this project.
The system retrieves relevant text from the 10-K filing and generates answers grounded in the document.

## ⚙️ How It Works

The system uses the Retrieval-Augmented Generation (RAG) pipeline:

Text Extraction:
Downloaded Apple’s 10-K HTML report from SEC EDGAR and cleaned it using Python and BeautifulSoup.
Inline XBRL tags (<ix:*>) and scripts were removed.

Chunking & Embeddings:
Split the text into smaller parts (~800 words each).
Converted them into embeddings using the sentence-transformers/all-MiniLM-L6-v2 model.

Similarity Search:
Used FAISS to find the most relevant chunks for each question based on cosine similarity.

LLM Integration:
Used Ollama running Llama 3 locally on my Mac M2 to generate answers from the retrieved text.

## 💬 Example Questions

You can ask the system questions like:

1. How does Apple describe its strategy for managing international sales and currency risks?
2. What steps does Apple mention for ensuring supply chain resilience and component availability?
3. What legal proceedings or regulatory risks are discussed in the filing?


The system retrieves the related paragraphs and produces short, cited answers from the 10-K text.

## 🧾 Evaluation

Relevance (Cosine Similarity): 0.43–0.48 → moderately relevant retrieval.

Faithfulness: Answers stayed close to retrieved context, with no hallucination.

Recall@5: All 3 sample questions retrieved correct information within top 5 chunks.

## 🧩 Tools & Libraries
Purpose	Tool
Text Download & Cleaning	requests, BeautifulSoup4
Embeddings	sentence-transformers
Vector Store	faiss-cpu
Language Model	Ollama (Llama 3)
Evaluation	numpy, matplotlib
🖥️ How to Run Locally
1. Clone this repository
git clone https://github.com/mehluli92/rag-apple-10k.git
cd rag-apple-10k

2. Create and activate a virtual environment
python3 -m venv venv
source venv/bin/activate

3. Install dependencies
pip install -r requirements.txt


(or manually install: sentence-transformers, faiss-cpu, ollama, beautifulsoup4, numpy)

4. Run Ollama and pull a model
brew install ollama
ollama serve
ollama pull llama3

5. Run the notebook

## Open Jupyter Lab:

jupyter lab


Then open RAGPipeline.ipynb and run the cells.
