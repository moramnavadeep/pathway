
# Real-Time BREAKING NEWS News Q\\&A with Pathway RAG CHAT BOT

here is working video https://drive.google.com/file/d/1G_Nxs2svaDCi3doKFNl-qzYJhRS8d_ar/view

This code showcases how to deploy a **Retrieval-Augmented Generation (RAG)** pipeline with [Pathway](https://pathway.com/) for **live question answering** on news data.
Rather than using static datasets, this system ingests the most recent articles from **NewsAPI**, indexes them in **Pathway's document store**, and responds to user questions with a Hugging Face **question-answering model**.

---

## Features

* **Live data ingestion**: Ingests news headlines/articles directly from [NewsAPI](https://newsapi.org/).
* **Automated text processing**: Cleans, tokenizes, and embeds articles.
* **High-performance retrieval**: Utilizes **Pathway's UsearchKnn retriever** to achieve semantic search at high speeds.
* **Question Answering**: A Hugging Face QA model (`distilbert-base-uncased-distilled-squad`) pulls out direct answers from context.
* **Source transparency**: Original news article URLs are given in answers.

---

## ⚙️ Architecture

```mermaid
flowchart TD
    A[User Query: "What is the latest news on AI?"] --> B[RAG Engine]
    B --> C[Retriever fetches News Articles]
    C --> D[Embedder encodes docs]
    D --> E[Vector DB / USearch]
    E --> F[Relevant Context + URL]
    F --> G[LLM (Question Answering)]
    G --> H[Final Answer with Sources]

```

1. **NewsAPI fetch** – gets the most recent articles in JSON.
2. **Data preparation** – cleans text, extracts fields, adds URLs.
3. **Pathway Document Store** – stores, splits, and embeds documents.
4. **Retriever** – identifies the most relevant text chunks to the user query.
5. **Hugging Face QA Model** – pulls exact answers.
6. **Response** – user receives an answer with source credit.

---

## Installation

```bash
pip install pathway sentence-transformers transformers requests pandas beautifulsoup4
```

---

## Environment Variables

You require a valid [NewsAPI key](https://newsapi.org/).
Either set it hard-coded in the script or in a `.env` file:

```env
NEWS_API_KEY=your_api_key_here
```

Then import it in Python with:

```python
from dotenv import load_dotenv
import os
load_dotenv()
NEWS_API_KEY = os.getenv("NEWS_API_KEY")
```

---

## ▶️ Usage

Execute the notebook/script:

```python
ask("latest medical field achievements?")
ask("UNO news")
```

Example output:

```
Answer: "Researchers created a new cancer treatment."
(Source: https://www.example-news.com/article123)

```

---

## Why Pathway?

While static pipelines are typical of traditional approaches, **Pathway** allows for:

* **Streaming ingestion** of live data streams (e.g., APIs, databases, logs).
* **Efficient indexing & retrieval** using `UsearchKnnFactory`.
* **Composable RAG** pipelines with simple integration into **Hugging Face models**.

This makes it well-suited for **real-time knowledge retrieval systems** like live news, finance, or monitoring use cases.

---

## Next Steps

* Deploy as an API endpoint (FastAPI/Flask).
* Support for multiple news sources added.
* Expanded to summarization + QA hybrid.
* Run on GPU for accelerated inference.

---

## Tech Stack

* **Pathway** – streaming data + retrieval
* **SentenceTransformers** – embeddings (`all-MiniLM-L6-v2`)
* **Transformers (Hugging Face)** – QA pipeline (`distilbert-base-uncased-distilled-squad`)
* **NewsAPI** – live data source
* **Pandas** – preprocessing
* **BeautifulSoup** – text cleaning

---

## License

MIT License. Feel free to use and modify.


