# 🧠 AI Knowledge Assistant with Conversational Memory (RAG Pipeline)

[![Python](https://img.shields.io/badge/Python-3.10%2B-blue.svg)](https://www.python.org/)
[![Framework](https://img.shields.io/badge/LangChain-0.2%2B-green.svg)](https://www.langchain.com/)
[![Vector Store](https://img.shields.io/badge/Qdrant-Cloud-red.svg)](https://qdrant.tech/)
[![LLM](https://img.shields.io/badge/LLM-Qwen2.5--3B-orange.svg)](https://huggingface.co/Qwen/Qwen2.5-3B-Instruct)
[![License](https://img.shields.io/badge/License-MIT-brightgreen.svg)](LICENSE)

An enterprise-grade **Retrieval-Augmented Generation (RAG)** system designed to integrate heterogeneous knowledge sources (PDF documents and structured Google Sheets / CSV data), index them into **Qdrant Cloud**, and answer natural language queries using a local HuggingFace LLM (**Qwen 2.5-3B**) with multi-turn conversational memory.

---

## 🏗️ System Architecture

```mermaid
graph TD
    subgraph Data Ingestion
        A[PDF Documents] --> C[Document Loaders]
        B[Google Sheets / CSV] --> C
    end

    subgraph Vector Indexing
        C --> D[Recursive Character Text Splitter]
        D --> E[HuggingFace Embeddings\nall-MiniLM-L6-v2]
        E --> F[(Qdrant Cloud Vector DB)]
    end

    subgraph RAG & Conversational Pipeline
        G[User Query] --> H[Similarity Search]
        F --> H
        H --> I[Retrieved Context Chunks]
        G --> J[Memory Manager\nBuffer + Summary]
        I --> K[Prompt Builder]
        J --> K
        K --> L[Qwen2.5-3B Instruct Model]
        L --> M[Contextual Response + Source Attribution]
    end
```

---

## ✨ Key Features

- **Multi-Source Data Integration:** Seamlessly ingests unstructured text (PDF lectures/reports) and structured data (housing prices / tables from Google Sheets).
- **High-Performance Vector Storage:** Utilizes **Qdrant Cloud** with `sentence-transformers/all-MiniLM-L6-v2` for ultra-fast semantic similarity retrieval.
- **Dual-Tier Conversational Memory:**
  - **Buffer Memory:** Retains exact recent conversation history for instant follow-up questions.
  - **Summary Memory:** Dynamically compresses older dialogue history into concise key facts to prevent context window overflow.
- **Strict Groundedness & Source Attribution:** Ensures answers are strictly derived from retrieved context while returning exact source metadata (e.g., PDF page, Sheet row).
- **Kaggle / Colab GPU Ready:** Fully optimized to run on T4 GPU environments with minimal latency.

---

## 📁 Repository Structure

```
.
├── AI_Knowledge_Assistant_with_Memory.ipynb  # Primary production notebook (Clean code)
├── Midterm_AI_Knowledge_Assistant.ipynb       # Full executed notebook with outputs & logs
├── Mid-term Project.pdf                      # Project assignment specifications & PDF data
├── requirements.txt                          # Production dependency specifications
├── .gitignore                                # Git exclusion configurations
└── README.md                                 # Project documentation
```

---

## 🚀 Quick Start Guide

### 1. Prerequisites & Installation

Clone the repository and install the dependencies:

```bash
git clone https://github.com/mo1gaber/AI_Knowledge_Assistant.git
cd AI_Knowledge_Assistant
pip install -r requirements.txt
```

### 2. Environment Configuration

The pipeline requires access to **Qdrant Cloud** for vector indexing. Set up the following environment variables (or add them via **Kaggle Secrets** / `.env`):

```bash
export QDRANT_URL="https://your-qdrant-cluster.cloud.qdrant.io"
export QDRANT_API_KEY="your-qdrant-api-key"
```

### 3. Running the Pipeline

Open the main notebook in Jupyter Notebook, VS Code, or Kaggle:

```bash
jupyter notebook AI_Knowledge_Assistant_with_Memory.ipynb
```

---

## 🧪 Evaluation & Testing Highlights

The pipeline includes automated tests evaluating:
1. **Factual Retrieval Accuracy:** Querying specific housing prices from tabular data.
2. **Domain Q&A:** Querying computer vision concepts from lecture slides.
3. **Conversational Memory:** Preserving user identity and context across 5+ dialogue turns.
4. **Hallucination Prevention:** Correctly reporting when requested information is absent from the knowledge base.

---

## 🛠️ Technology Stack

- **Orchestration:** LangChain Core, LangChain Community, LangChain Qdrant
- **Vector Database:** Qdrant Cloud Engine
- **Embeddings Model:** `sentence-transformers/all-MiniLM-L6-v2`
- **Large Language Model:** `Qwen/Qwen2.5-3B-Instruct`
- **Frameworks:** PyTorch, Transformers, Accelerate, Pandas, PyPDF

---

## 👤 Author

- **Mohamed Gaber** (`mo1gaber`) - [GitHub Profile](https://github.com/mo1gaber)
- **Email:** `modym8375@gmail.com`