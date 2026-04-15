# Contributing to Product Metadata Intelligence Platform

Thank you for your interest in contributing! Here's how to get started.

---

## 🛠️ Setting Up for Development

```bash
git clone https://github.com/YOUR_USERNAME/product-metadata-platform.git
cd product-metadata-platform
python -m venv venv
source venv/bin/activate       # Windows: venv\Scripts\activate
pip install -r requirements.txt
cp .env.example .env           # Add your API key
```

---

## 🔄 Workflow

1. **Fork** the repository
2. **Create a branch** for your feature or fix:
   ```bash
   git checkout -b feature/your-feature-name
   ```
3. **Make your changes** and write/update tests where relevant
4. **Run the test suite** before submitting:
   ```bash
   pytest tests/ -v
   ```
5. **Commit** with a clear message:
   ```bash
   git commit -m "feat: add support for XLSX supplier documents"
   ```
6. **Push** and open a **Pull Request** against `main`

---

## ✅ Code Standards

- Follow **PEP 8** style — use `black` for formatting if possible
- Add **docstrings** to all new functions and classes
- Write **tests** for new features in `tests/`
- Keep functions focused — one responsibility per function
- Use **type hints** throughout

---

## 🧪 Running Tests

```bash
# Run all tests
pytest tests/ -v

# Run with coverage report
pytest tests/ -v --cov=src --cov-report=term-missing
```

---

## 📁 Where to Put Things

| What | Where |
|---|---|
| Document parsing logic | `src/extractor/document_parser.py` |
| LLM extraction / schema | `src/extractor/metadata_extractor.py` |
| Compliance rules | `src/extractor/validator.py` |
| Vector store / RAG | `src/rag/rag_engine.py` |
| Streamlit UI | `src/ui/app.py` |
| Tests | `tests/` |

---

## 🐛 Reporting Bugs

Please open a GitHub Issue with:
- A clear description of the bug
- Steps to reproduce
- Expected vs actual behaviour
- Your Python version and OS

---

## 💡 Feature Ideas

Check the **Roadmap** section in the README for planned features. If you'd like to work on one, open an Issue first so we can discuss the approach before you start coding.

---

## 📄 License

By contributing, you agree that your contributions will be licensed under the MIT License.
