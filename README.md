# 🤖 RAG Chatbot over LinkR Documentation (LangChain + Chroma + GPT-3.5)

This project implements a **Retrieval-Augmented Generation (RAG)** chatbot over the documentation and source code of the R package **LinkR**. It uses **LangChain**, **GPT-3.5**, and a **Chroma vector database** to provide contextualized answers from a custom documentation knowledge base.

---

## 🎯 Objective

To create a chatbot that can **answer questions in natural language** based on the internal documentation and source code of `LinkR` — using the principles of **RAG**, where the LLM is grounded in external data it retrieves in real time.

---

## 🧩 RAG Pipeline Overview

### 1. 🗂️ Document Loading

The bot loads and aggregates multiple types of documentation:

- `Readme.md`
- `DESCRIPTION` file
- Help scripts (`help_*.R`)
- Manual documentation files (`.Rd`)
- Source code files (`.R`)

Loaders used:
- `UnstructuredMarkdownLoader` (for Markdown)
- `TextLoader` (for plain text and code)

---

### 2. ✂️ Text Splitting

- `RecursiveCharacterTextSplitter` is used to split documents into ~500-character chunks
- Optionally: `MarkdownHeaderTextSplitter` helps preserve logical structure

---

### 3. 🧠 Embedding & Indexing

- Uses **`all-MiniLM-L6-v2`** (SentenceTransformers) to convert chunks to embeddings
- Vectors are stored in **Chroma**, enabling fast semantic search and retrieval

---

### 4. 💬 Retrieval-Augmented Generation (RAG)

- Questions are processed using **LangChain’s RetrievalQA** chain
- `gpt-3.5-turbo` (via `ChatOpenAI`) generates answers based on retrieved documents

> ✨ Unlike pure LLM prompts, the chatbot bases its answers only on the indexed LinkR documentation — ensuring traceable, grounded responses.

---

## ✅ Example

```python
qa({"query": "What does the LinkR package do?"})
```

---

## 📁 Project Files

| File | Description |
|------|-------------|
| `Chatbot_LinkR.ipynb` | Jupyter notebook with full pipeline |
| `/R`, `/man`, `DESCRIPTION`, `README.md` | Files indexed by the RAG pipeline |

---

## 🛠️ Tech Stack

- Python + LangChain
- OpenAI GPT-3.5 via `ChatOpenAI`
- Chroma (Vector DB)
- SentenceTransformers
- dotenv for API key management

---

## 👩‍💻 Author

DataForGood -
Chloé Petridis  (contributor)
