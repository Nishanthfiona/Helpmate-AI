# HelpMate AI - Insurance Policy Q&A System

## Description
This project implements a Retrieval-Augmented Generation (RAG) system using Python, LangChain, and Google Gemini. It allows users to ask questions in natural language about the content of insurance policy documents (text-based PDFs) and receive answers grounded in the document text, complete with source citations.

## Features
- Loads multiple text-based PDF documents from a specified folder.
- Splits documents into manageable chunks for processing.
- Generates semantic embeddings using Google's Gemini embedding models.
- Stores embeddings and metadata persistently using ChromaDB.
- Retrieves relevant document chunks based on user queries using vector similarity search.
- Enhances retrieval relevance using a Cross-Encoder re-ranking model.
- Generates natural language answers using Google's Gemini generative models, based *only* on the retrieved context.
- Provides source document and page number citations for generated answers.
- Includes an interactive command-line loop for asking questions.

## Setup

1.  **Get Code:** Download or clone the project notebook (`HelpMate AI Project.ipynb`).
2.  **Install Dependencies:** Run the first code cell in the notebook to install required Python packages:
    ```bash
    !pip install -U -q langchain langchain-google-genai chromadb pdfplumber langchain-community sentence-transformers google-colab pypdf
    ```
3.  **Get API Key:** Obtain an API key for Google Gemini. You can usually get this from [Google AI Studio](https://aistudio.google.com/).
4.  **Configure API Key:** Set your Gemini API key in the notebook (Cell 3). Using Colab Secrets manager is recommended:
    * Click the key icon (🔑) in Colab's left sidebar.
    * Add a new secret named `GOOGLE_API_KEY`.
    * Paste your API key as the value.
    * Ensure 'Notebook access' is enabled.
    * Alternatively, provide the key when prompted by `getpass` if secrets aren't used.
5.  **Prepare Data Folder:**
    * Create a folder in your Google Drive (or locally). An example path used in the notebook is `/content/drive/MyDrive/HelpMate AI Codes`.
    * **Important:** Place only **text-based** PDF files (like `icici-bharat-griha-raksha-policy.pdf`) in this folder. The current version does not support image-based/scanned PDFs requiring OCR.
6.  **Update Paths:** In Cell 3 of the notebook, verify or modify the `pdf_directory_path` variable to point to your data folder. You can also modify `chroma_persist_path` if you want to store the vector database elsewhere (default example: `/content/drive/MyDrive/HelpMate AI Codes/chroma_db_langchain`).

## Running

1.  Open the `HelpMate AI Project.ipynb` notebook in a compatible environment (e.g., Google Colab).
2.  Ensure your Google Drive is mounted if using Drive paths (Cell 2 handles this).
3.  Execute the cells sequentially from top to bottom.
    * Cell 7/8 (Vector Store creation/loading) will build the ChromaDB database the first time it's run with new data. This may take some time depending on document size and embedding calls. On subsequent runs, it should load the existing store if the path is unchanged.
    * Cell 15 starts the interactive query loop.
4.  Enter your questions about the loaded policy documents when prompted.
5.  Type `quit` to exit the query loop.

## Key Technologies & Libraries

* Python 3
* LangChain (Core, Google GenAI, Community)
* Google Gemini API (via `langchain-google-genai`)
* ChromaDB (Vector Store)
* Sentence Transformers (for Cross-Encoder model)
* PyPDF (via `langchain-community` for PDF loading)
* Google Colab (Development Environment)

## Limitations

* **Text-Based PDFs Only:** The current document loader (`PyPDFDirectoryLoader`) is optimized for PDFs where text can be directly extracted. It does not perform OCR and will not effectively process image-based or scanned documents.
* **Performance:** Embedding generation (first run of Cell 7/8) and potentially complex queries can take time depending on document size, API response times, and the computational resources of the execution environment.
* **API Costs/Quotas:** Use of the Google Gemini API for embeddings and generation is subject to Google's pricing and free tier limits. Ensure you have sufficient quota or billing enabled.

