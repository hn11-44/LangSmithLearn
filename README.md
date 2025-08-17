# LangSmithLearn 🚀

Welcome to **LangSmithLearn**, a repository dedicated to my hands-on journey of building, debugging, and understanding Retrieval-Augmented Generation (RAG) applications. This project was developed as a deep dive into the LangChain ecosystem, with a strong focus on applying modern **LLMOps** principles like observability and evaluation using **LangSmith**.

*Project developed in Milan, Italy - August 2025.*

## 📜 Core Concepts & Technologies

This repository showcases a practical application of the following state-of-the-art tools and concepts:

* **Framework:** LangChain
* **LLM:** Google Gemini API (`gemini-1.5-flash-latest`, `embedding-001`)
* **Observability & Evaluation:** LangSmith (Tracing, Debugging, and Reporting)
* **Core Architecture:** Retrieval-Augmented Generation (RAG)
* **Vector Stores:** FAISS and Chroma
* **Data Ingestion:** Automated Web Scraping (`SitemapLoader`, `BeautifulSoup`)
* **Environment & Package Management:** `uv`
* **Development Environment:** Jupyter Notebooks in VS Code

---

## 🤖 Projects Overview

This repository contains two primary projects, demonstrating a clear progression in complexity.

### 1. Simple RAG Application

This is the "Hello, World!" of RAG. A foundational script designed to teach the absolute basics of the RAG pipeline.

* **Knowledge Base:** A simple, hardcoded Python list of sentences.
* **Goal:** To understand the fundamental flow: `Load -> Embed -> Store -> Retrieve -> Generate`.
* **Key Feature:** Demonstrates the core logic of connecting a retriever, a prompt template, and an LLM into a single chain.

### 2. The Dankoe Letters Bot (Advanced RAG)

This is a more realistic, end-to-end RAG application that tackles the challenges of working with real-world, messy data from a live website.

* **Knowledge Base:** Multiple articles scraped from Dan Koe's newsletter, "[The Dankoe Letters](https://letters.thedankoe.com/)".
* **Goal:** To build a robust, observable, and accurate Q&A bot capable of answering philosophical and business-related questions based on the author's writings.
* **Key Features:**
    * **Automated Data Ingestion:** Uses a `SitemapLoader` to automatically discover all relevant article URLs.
    * **Surgical Data Extraction:** Implements a custom parser with `BeautifulSoup` to isolate the main article content, removing "noise" like headers, footers, ads, and comment sections.
    * **Functional & Traceable Design:** The entire pipeline is built with modular, traceable functions (`@traceable`), making the logic clear and highly observable in LangSmith.

---

## 🛠️ Getting Started

Follow these steps to set up the environment and run the projects yourself.

### Prerequisites

* Python 3.10+
* `uv` package manager (or you can use `pip`)

### 1. Clone the Repository

```bash
git clone [https://github.com/your-username/LangSmithLearn.git](https://github.com/your-username/LangSmithLearn.git)
cd LangSmithLearn
```

### 2. Set Up the Environment

This project uses `uv` for fast environment and package management.

```bash
# Create a virtual environment
uv venv

# Activate the environment
# On macOS or Linux:
source .venv/bin/activate
# On Windows:
# .venv\Scripts\activate
```

### 3. Install Dependencies

Install all the required packages using the `requirements.txt` file.

```bash
# The requirements.txt file should be created from our working project
uv pip install -r requirements.txt
```

### 4. Configure Your API Keys

This project requires API keys for Google Gemini and LangSmith. The best practice is to use a `.env` file.

1.  Create a file named `.env` in the root of the project directory.
2.  Add your keys to this file like so:

    ```env
    # .env file
    GOOGLE_API_KEY="YOUR_GOOGLE_API_KEY_HERE"
    LANGCHAIN_API_KEY="YOUR_LANGSMITH_API_KEY_HERE"
    USER_AGENT="YourAppName/1.0 (contact: your.email@example.com)"
    ```
    *(Note: The notebooks use `getpass` for interactive key entry, but using a `.env` file with `python-dotenv` is the recommended practice for scripts.)*

### 5. Run the Notebooks

Open the project in VS Code or your preferred editor and run the Jupyter Notebooks (`.ipynb` files) cell by cell.

---

## 💡 Key Learnings & LLMOps Insights

This project was a deep dive into the practical realities of building RAG systems. The most critical takeaways were:

1.  **Observability is Non-Negotiable:** Setting up LangSmith from the very beginning was crucial. It allowed for instant visualization of the chain's execution, making it possible to diagnose complex issues.
2.  **"Garbage In, Garbage Out":** The single biggest factor in RAG quality is the quality of the ingested data. The transition from a naive web scraper to a "surgical" parser that removes noise was the most significant improvement made.
3.  **Debugging is a Process of Elimination:** We encountered multiple types of errors:
    * **Environment Errors** (`distutils`, `protobuf`, `asyncio` loop conflicts) which were solved by managing dependencies and restarting the kernel.
    * **Data Errors** (`IndexError` from empty lists) which were solved by inspecting the data source and correcting filters.
    * **Retrieval Quality Errors** (getting "I don't know" as an answer) which were solved by improving the data quality and retriever parameters.
4.  **Modular, Functional Code is Key:** Refactoring the pipeline into traceable functions (`@traceable`) dramatically improved the clarity of the code and the usefulness of the LangSmith traces.

## 🔮 Future Work

The "Dankoe Letters Bot" is a strong foundation. The next steps to improve its state-of-the-art capabilities would be to implement:

* **Advanced Retrieval Strategies:** Explore `SelfQueryRetriever` (to filter by article) or adding a `ReRanker` to improve the quality of the retrieved context.
* **Conversational Memory:** Add the ability for the bot to remember the last few questions and answer follow-ups.
* **Formal Evaluation:** Use the "Datasets & Testing" features in LangSmith to create a formal test set and score the bot's performance on metrics like correctness and relevance.