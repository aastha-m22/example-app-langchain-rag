# 🤖 RAG Chatbot — LangChain + Groq + Streamlit

A production-ready Retrieval-Augmented Generation (RAG) chatbot built with
**LangChain**, **Groq** (free & fast LLM inference), and **Streamlit**.
Upload your own documents, ask questions, and get grounded answers — all
running locally or on Streamlit Cloud.

---

## ✨ Features

- **Hybrid retrieval** — BM25 keyword search + Chroma vector search fused with
  Reciprocal Rank Fusion (RRF) for best-of-both results
- **Free embeddings** — `sentence-transformers/all-MiniLM-L6-v2` runs locally,
  no embedding API key needed
- **Groq LLM** — ultra-fast inference via `llama3-70b-8192` (free tier
  available)
- **Conversation memory** — chat history is preserved across turns in the
  Streamlit session
- **Zero OpenAI dependency** — completely removed

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| UI | Streamlit |
| LLM | Groq (`llama3-70b-8192`) |
| Orchestration | LangChain |
| Embeddings | HuggingFace `all-MiniLM-L6-v2` (local) |
| Vector store | Chroma |
| Keyword retrieval | BM25 (`rank-bm25`) |
| Hybrid fusion | LangChain `EnsembleRetriever` |

---

## 🚀 Quick Start

### 1 — Clone the repo

```bash
git clone https://github.com/<your-username>/example-app-langchain-rag.git
cd example-app-langchain-rag
```

### 2 — Create a virtual environment

```bash
# Windows
python -m venv venv
venv\Scripts\activate

# macOS / Linux
python -m venv venv
source venv/bin/activate
```

### 3 — Install dependencies

```bash
pip install -U pip
pip install -r requirements.txt
```

### 4 — Get a free Groq API key

1. Visit <https://console.groq.com>
2. Sign up / log in
3. Create an API key

### 5 — Set up secrets

```bash
mkdir .streamlit
cp .streamlit/secrets.toml.example .streamlit/secrets.toml   # or create manually
```

Edit `.streamlit/secrets.toml`:

```toml
GROQ_API_KEY = "gsk_your_key_here"
```

> **Tip:** You can also paste the key directly into the sidebar at runtime —
> no file needed for local testing.

### 6 — Add your documents

Drop `.txt`, `.pdf`, or `.md` files into the `data/` directory.

### 7 — Run the app

```bash
streamlit run streamlit_app.py
```

---

## ☁️ Deploy to Streamlit Cloud

1. Push your fork to GitHub
2. Go to <https://share.streamlit.io> → **New app**
3. Point it at `streamlit_app.py`
4. In **Advanced settings → Secrets**, add:
   ```
   GROQ_API_KEY = "gsk_your_key_here"
   ```
5. Deploy 🎉

---

## 📁 Project Structure

```
├── streamlit_app.py      # Main Streamlit UI
├── basic_chain.py        # LLM initialisation (Groq)
├── full_chain.py         # Full RAG + memory chain
├── ensemble.py           # Hybrid BM25 + vector retriever
├── rag_chain.py          # RAG chain builder
├── memory.py             # Conversation memory wrapper
├── local_loader.py       # Load files from data/
├── remote_loader.py      # Load web pages
├── splitter.py           # Document splitting
├── vector_store.py       # Chroma vector DB helpers
├── data/                 # ← put your documents here
├── examples/             # Sample documents
├── requirements.txt
└── .streamlit/
    └── secrets.toml      # API keys (git-ignored)
```

---

## 🔧 Configuration

| Variable | Where | Description |
|---|---|---|
| `GROQ_API_KEY` | `.streamlit/secrets.toml` or sidebar | Groq API key |

---

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch: `git checkout -b feat/my-feature`
3. Commit your changes: `git commit -m "feat: add my feature"`
4. Push: `git push origin feat/my-feature`
5. Open a Pull Request

---

## 📄 License

[Apache 2.0](LICENSE)

---

## 🙏 Acknowledgements

- [Streamlit](https://streamlit.io) for the original example app
- [LangChain](https://langchain.com) for the RAG framework
- [Groq](https://groq.com) for blazing-fast free LLM inference
