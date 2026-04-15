# 🏗️ Product Metadata Intelligence Platform

> An AI-powered platform that automatically extracts, structures, and enables intelligent search over supplier product data — built with LLMs, NLP, and RAG.

[![Python](https://img.shields.io/badge/Python-3.10+-blue.svg)](https://python.org)
[![LangChain](https://img.shields.io/badge/LangChain-0.2+-green.svg)](https://langchain.com)
[![Streamlit](https://img.shields.io/badge/Streamlit-1.35+-red.svg)](https://streamlit.io)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

---

## 🎯 Problem Statement

Design and procurement teams in architecture/interiors firms spend significant time manually collecting, validating, and organising product information from hundreds of supplier documents (PDFs, datasheets, spreadsheets). This project replaces that fragmented manual process with an AI-driven pipeline that:

- **Automatically extracts** structured product metadata from unstructured supplier documents
- **Validates and normalises** product attributes (dimensions, materials, compliance certifications, sustainability data)
- **Enables intelligent search** using vector embeddings and Retrieval-Augmented Generation (RAG)
- **Answers natural language queries** about products, specs, and compliance

---

## 🏛️ Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                    Streamlit Frontend                        │
│         (Upload docs | Search | Ask questions)              │
└────────────────────────┬────────────────────────────────────┘
                         │
         ┌───────────────┼───────────────┐
         ▼               ▼               ▼
  ┌─────────────┐ ┌─────────────┐ ┌─────────────┐
  │  Document   │ │   Vector    │ │     RAG     │
  │  Extractor  │ │    Store    │ │   Engine    │
  │  (NLP/LLM)  │ │  (FAISS)   │ │  (LangChain)│
  └─────────────┘ └─────────────┘ └─────────────┘
         │               │               │
         └───────────────┼───────────────┘
                         ▼
              ┌─────────────────────┐
              │   Structured JSON   │
              │   Product Metadata  │
              │   (SQLite / Export) │
              └─────────────────────┘
```

---

## ✨ Features

| Feature | Description | Status |
|---|---|---|
| 📄 PDF/Text Ingestion | Upload supplier datasheets, parse with OCR fallback | ✅ |
| 🧠 LLM Metadata Extraction | Extract product name, dimensions, materials, certs via LLM | ✅ |
| 🔍 Vector Search | Semantic similarity search across all products | ✅ |
| 💬 RAG Q&A | Ask natural language questions ("Show me FSC certified timber panels") | ✅ |
| ✅ Compliance Check | Flag products missing key sustainability/compliance fields | ✅ |
| 📊 Product Directory | Searchable, filterable product metadata table | ✅ |
| 📤 Export | Download structured metadata as CSV/JSON | ✅ |

---

## 🚀 Quick Start

### 1. Clone the repo
```bash
git clone https://github.com/YOUR_USERNAME/product-metadata-platform.git
cd product-metadata-platform
```

### 2. Create virtual environment
```bash
python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate
```

### 3. Install dependencies
```bash
pip install -r requirements.txt
```

### 4. Set up environment variables
```bash
cp .env.example .env
# Edit .env and add your OpenAI API key (or use local Ollama - see below)
```

### 5. Run the app
```bash
streamlit run src/ui/app.py
```

### 🆓 Run with FREE local LLM (Ollama)
```bash
# Install Ollama: https://ollama.com
ollama pull llama3.2
# Set in .env: LLM_PROVIDER=ollama
streamlit run src/ui/app.py
```

---

## 📁 Project Structure

```
product-metadata-platform/
│
├── src/
│   ├── extractor/
│   │   ├── __init__.py
│   │   ├── document_parser.py      # PDF/text parsing, OCR fallback
│   │   ├── metadata_extractor.py   # LLM-based structured extraction
│   │   └── validator.py            # Schema validation & compliance checks
│   │
│   ├── rag/
│   │   ├── __init__.py
│   │   ├── embeddings.py           # Vector embedding pipeline
│   │   ├── vector_store.py         # FAISS index management
│   │   └── rag_engine.py           # RAG Q&A chain
│   │
│   └── ui/
│       ├── app.py                  # Main Streamlit app
│       └── components.py           # Reusable UI components
│
├── data/
│   └── sample_docs/                # Sample supplier PDFs for demo
│
├── tests/
│   ├── test_extractor.py
│   └── test_rag.py
│
├── docs/
│   └── architecture.md
│
├── requirements.txt
├── .env.example
├── config.py
└── README.md
```

---

## 🧠 Technical Deep Dive

### Metadata Extraction Pipeline

The extractor uses a **structured LLM output** approach with Pydantic validation:

1. **Document Parsing** — PyMuPDF extracts text; pytesseract handles scanned PDFs via OCR
2. **Chunking** — Documents split into semantic chunks preserving context
3. **LLM Extraction** — GPT-4o / Llama3 extracts structured fields using a typed Pydantic schema
4. **Validation** — Each extracted product is validated against compliance rules

```python
class ProductMetadata(BaseModel):
    product_name: str
    manufacturer: str
    category: str
    dimensions: Optional[dict]
    materials: List[str]
    certifications: List[str]      # FSC, ISO, CE, BREEAM, etc.
    sustainability_score: Optional[float]
    carbon_footprint: Optional[str]
    compliance_flags: List[str]
```

### RAG Search Engine

- **Embeddings**: `text-embedding-3-small` (OpenAI) or `nomic-embed-text` (local)
- **Vector Store**: FAISS for fast similarity search
- **Retrieval**: Top-K semantic search + metadata filtering
- **Generation**: Context-grounded answers with source citations

---

## 📊 Demo Screenshots

> Upload a supplier PDF → Get structured metadata instantly → Ask questions in natural language

*See `/docs/screenshots/` for full demo walkthrough*

---

## 🗺️ Roadmap

- [ ] BIM/IFC format export for design tool integration
- [ ] Multi-supplier batch processing pipeline
- [ ] Automated sustainability report generation
- [ ] REST API for integration with external tools
- [ ] Docker containerisation for deployment
- [ ] Fine-tuned extraction model on domain-specific data

---

## 🤝 Contributing

Pull requests are welcome! Please read [CONTRIBUTING.md](docs/CONTRIBUTING.md) first.

---

## 📄 License

MIT License — see [LICENSE](LICENSE) for details.

---

## 👤 Author

Built as a portfolio project demonstrating AI-powered data extraction and RAG systems applied to the built environment / interior design domain.
