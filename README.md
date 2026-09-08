# 🇮🇳 Lok Sabha RAG — Retrieval-Augmented Question Answering

A **Retrieval-Augmented Generation (RAG)** system built to retrieve and answer questions from **Lok Sabha parliamentary proceedings** using semantic search, vector embeddings, FAISS, and a generative language model.

The project processes parliamentary documents, converts them into searchable semantic chunks, generates dense vector embeddings, performs similarity-based retrieval using **FAISS**, and uses the retrieved context to generate grounded answers.

---

## 📌 Overview

Parliamentary proceedings contain a large volume of information distributed across thousands of documents. Finding relevant information through conventional keyword-based search can be difficult when the user's query does not exactly match the wording used in the proceedings.

This project addresses that problem using a **semantic retrieval + generative AI pipeline**.

A user can ask a natural-language question, and the system:

```text
User Query
    ↓
Query Embedding
    ↓
FAISS Similarity Search
    ↓
Relevant Parliamentary Passages
    ↓
Context Construction
    ↓
Generative Language Model
    ↓
Grounded Answer
```

---

## 🎯 Objectives

* Build a semantic search system over Lok Sabha proceedings.
* Process and organize parliamentary documents into searchable chunks.
* Generate dense semantic embeddings using **Sentence Transformers**.
* Build an efficient vector index using **FAISS**.
* Retrieve relevant parliamentary passages for natural-language queries.
* Implement a **Retrieval-Augmented Generation (RAG)** pipeline.
* Evaluate retrieval behavior across different query types.
* Explore NLP and generative AI techniques alongside the main RAG pipeline.

---

## ✨ Key Features

### 🔎 Semantic Retrieval

Instead of relying only on exact keyword matches, the system represents documents and queries as dense vectors and retrieves semantically similar passages.

### 🧠 Retrieval-Augmented Generation

Retrieved parliamentary passages are provided as context to the generative model, allowing responses to be grounded in the underlying proceedings.

### 📚 Large-Scale Document Processing

The pipeline processes a large collection of Lok Sabha proceedings and divides the extracted content into manageable semantic chunks.

### ⚡ FAISS Vector Search

**FAISS (Facebook AI Similarity Search)** is used for efficient similarity search over the generated embeddings.

The project uses an `IndexFlatIP` index for inner-product similarity search.

### 📊 Retrieval Evaluation

The project includes experiments for analyzing retrieval behavior and comparing retrieval performance across different query categories.

### 🧪 NLP Experiments

Additional experiments explore transformer-based NLP capabilities including text generation, summarization, and question answering.

---

## 🏗️ System Architecture

```text
                 ┌─────────────────────────┐
                 │   Lok Sabha Documents   │
                 │     / Proceedings       │
                 └────────────┬────────────┘
                              │
                              ▼
                 ┌─────────────────────────┐
                 │   Document Extraction   │
                 │      & Cleaning         │
                 └────────────┬────────────┘
                              │
                              ▼
                 ┌─────────────────────────┐
                 │     Text Chunking       │
                 │    + Metadata Creation  │
                 └────────────┬────────────┘
                              │
                              ▼
                 ┌─────────────────────────┐
                 │ SentenceTransformer     │
                 │     Embeddings          │
                 └────────────┬────────────┘
                              │
                              ▼
                 ┌─────────────────────────┐
                 │      FAISS Index        │
                 │      IndexFlatIP        │
                 └────────────┬────────────┘
                              │
                    ┌─────────┴─────────┐
                    │                   │
                    ▼                   ▼
              User Query          Stored Vectors
                    │
                    ▼
            Query Embedding
                    │
                    ▼
             FAISS Retrieval
                    │
                    ▼
          Top Relevant Passages
                    │
                    ▼
          Context Construction
                    │
                    ▼
          Generative Language Model
                    │
                    ▼
             Final Answer
```

---

## 🔄 RAG Pipeline

### 1. Data Collection

Lok Sabha parliamentary proceedings are collected and prepared for downstream processing.

### 2. Document Extraction

PDF documents are processed and their textual content is extracted using PDF processing tools.

### 3. Text Processing

Extracted text is cleaned and divided into smaller chunks while retaining relevant metadata.

### 4. Embedding Generation

Each text chunk is converted into a dense vector representation using a **Sentence Transformer** model.

### 5. Vector Indexing

The generated embeddings are stored in a FAISS index.

```text
Text Chunk
    ↓
Sentence Transformer
    ↓
Embedding Vector
    ↓
FAISS Index
```

### 6. Query Processing

When a user submits a question, the query is converted into an embedding using the same embedding model.

### 7. Similarity Search

FAISS performs similarity search and retrieves the most relevant passages.

The implemented retrieval pipeline uses a default **Top-K of 5 results**.

### 8. Context-Augmented Generation

The retrieved passages are combined into a context and supplied to the generative model.

### 9. Answer Generation

The language model generates a natural-language answer based on the retrieved parliamentary context.

---

## 🗂️ Repository Structure

```text
lok-sabha-rag/
│
├── notebooks/
│   ├── 01_data_scraping.ipynb
│   ├── 02_data_processing_and_indexing.ipynb
│   ├── 03_rag_pipeline_and_evaluation.ipynb
│   └── 04_nlp_experiments.ipynb
│
├── docs/
│   └── architecture.png
│
├── screenshots/
│
├── .gitignore
├── requirements.txt
└── README.md
```

### Notebook Workflow

| Notebook                                | Purpose                                                                  |
| --------------------------------------- | ------------------------------------------------------------------------ |
| `01_data_scraping.ipynb`                | Data collection, extraction, cleaning, chunking and metadata preparation |
| `02_data_processing_and_indexing.ipynb` | Embedding generation and FAISS vector indexing                           |
| `03_rag_pipeline_and_evaluation.ipynb`  | Semantic retrieval, RAG generation and evaluation                        |
| `04_nlp_experiments.ipynb`              | Additional transformer-based NLP and GenAI experiments                   |

---

## 🛠️ Technology Stack

### Programming

* Python

### Data Processing

* Pandas
* BeautifulSoup
* Requests
* pdfplumber
* tqdm

### Machine Learning / NLP

* Sentence Transformers
* Hugging Face Transformers
* PyTorch

### Vector Search

* FAISS

### Generative AI

* Google Gemini API

### Development Environment

* Google Colab
* Jupyter Notebooks

### Visualization & Evaluation

* Matplotlib
* PCA-based embedding visualization
* Retrieval-time analysis

---

## 📊 Retrieval & Evaluation

The project includes experiments to analyze the retrieval pipeline and understand how the system behaves for different types of questions.

The evaluation workflow examines:

* Query types
* Retrieval performance
* Search latency
* Retrieved passages
* Embedding-space behavior
* Similarity-based ranking

This helps analyze not only whether the system can generate an answer, but also whether the **retrieval stage is bringing relevant parliamentary context into the generation pipeline**.

---

## 💡 Example Query Flow

Example:

```text
User:
"What discussions were held regarding a particular
government policy?"
```

The system performs:

```text
Question
   ↓
Generate Query Embedding
   ↓
FAISS Similarity Search
   ↓
Retrieve Top 5 Passages
   ↓
Construct Context
   ↓
Send Context + Question to LLM
   ↓
Generate Answer
```

This allows users to interact with a large parliamentary corpus using natural language rather than manually searching through individual documents.

---

## 🔐 Security & Credential Management

API credentials are **not stored directly in the notebooks**.

Secrets such as API keys and authentication tokens should be provided through environment variables or notebook secret management.

Example:

```python
import os
from google import genai

client = genai.Client(
    api_key=os.environ["GOOGLE_API_KEY"]
)
```

Never commit API keys, authentication tokens, private credentials, datasets containing sensitive information, or generated secret files to the repository.

---

## 🚀 Running the Project

### 1. Clone the repository

```bash
git clone https://github.com/ritika-kabiraj/lok-sabha-rag.git
cd lok-sabha-rag
```

### 2. Install dependencies

```bash
pip install -r requirements.txt
```

### 3. Open the notebooks

The recommended execution order is:

```text
01_data_scraping.ipynb
        ↓
02_data_processing_and_indexing.ipynb
        ↓
03_rag_pipeline_and_evaluation.ipynb
```

The notebooks can be executed using **Google Colab** or a compatible Jupyter environment.

---

## 📈 Future Improvements

* Add a dedicated web-based user interface.
* Introduce hybrid keyword + semantic retrieval.
* Experiment with different embedding models.
* Add reranking for retrieved passages.
* Implement citation-aware answers linking responses to source proceedings.
* Add persistent vector-database storage.
* Improve retrieval evaluation using standard IR metrics such as Precision@K, Recall@K and MRR.
* Add conversational multi-turn question answering.
* Support filtering by year, session, ministry, member, or parliamentary topic.
* Deploy the system as a production-ready RAG application.

---

## 🎓 Project Significance

This project demonstrates the application of **Retrieval-Augmented Generation to a large-scale public parliamentary knowledge base**.

It combines:

```text
Data Engineering
       +
Natural Language Processing
       +
Vector Search
       +
Information Retrieval
       +
Generative AI
```

The project provides practical experience in building an end-to-end pipeline for transforming unstructured documents into a searchable and generative knowledge system.

---

## 👩‍💻 Author

**Ritika Kabiraj**

Computer Science & Engineering

---

## 📜 Disclaimer

This project is intended for **educational and research purposes**. Generated answers should be verified against the original parliamentary proceedings before being used for official, legal, political, or research-critical purposes.
