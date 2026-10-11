# MultiPDFChat

A desktop RAG (Retrieval-Augmented Generation) application that lets you chat with multiple PDF files using Google Gemini embeddings and a FAISS vector index.To understand RAG and its architecture kindly refer the image attached with this project.

## Overview

This project reads one or more PDF documents, extracts text, splits it into chunks, creates vector embeddings, stores them in a FAISS index, and then answers questions based on the selected document content.

It is built with:
- Python
- PyPDF2 for PDF parsing
- LangChain + LangChain Google GenAI for embeddings and LLM interaction
- FAISS for vector search
- Tkinter for the PDF file selection dialog

## Features

- Select multiple PDF files from your system
- Extract text from all selected documents
- Split long documents into manageable chunks
- Create embeddings with Google Gemini
- Save and reuse a FAISS vector index locally
- Ask natural-language questions about the PDF content
- Use a conversational QA chain powered by Gemini

## Project Structure

```text
multiPDFChat/
├── app.py              # Main application logic
├── faiss_index/        # Local FAISS vector index folder
├── pdf1.pdf            # Example PDF file
├── pdf2.pdf            # Example PDF file
├── requirements.txt     # Python dependencies
├── .env                # Environment variables (not committed in production)
└── README.md           # Project documentation
```

## Prerequisites

Before running the project, make sure you have:
- Python 3.9 or later
- A Google API key from Google AI Studio / Gemini
- A local environment where Tkinter is available

## Setup

1. Clone or open the project folder.
2. Create and activate a virtual environment:

```bash
python -m venv .venv
.venv\Scripts\activate
```

3. Install the dependencies:

```bash
pip install -r requirements.txt
```

4. Create a `.env` file in the project root with your Google API key:

```env
GOOGLE_API_KEY=your_google_api_key_here
```

## Run the App

```bash
python app.py
```

A file dialog will open, allowing you to select one or more PDF files.

After selecting the PDFs, the app will:
- read the PDF text
- create chunks
- generate embeddings
- build the FAISS index
- prompt you with a Q&A loop

## How It Works

The workflow is:

1. User selects PDF files
2. Text is extracted page by page
3. Text is split into chunks using a recursive character splitter
4. Embeddings are generated with `GoogleGenerativeAIEmbeddings`
5. Documents are stored in a FAISS vector index
6. The user asks a question
7. The app searches for similar chunks
8. Gemini answers using the matched context

## Example Usage

```text
Ask a question (or type 'exit' to quit): What are the key benefits mentioned in the documents?
```

The app will retrieve the most relevant chunks and answer from that context.

## Notes

- The app creates or updates the local FAISS index in `faiss_index/`.
- If the PDFs are image-only or scanned documents without selectable text, extraction may fail or return empty content.
- This application is a desktop app and uses a GUI file picker, so it is best suited for local use.
- The app saves the vector store locally to avoid recomputing embeddings every time.

## Troubleshooting

### `GOOGLE_API_KEY not found in your .env file`
Make sure the `.env` file exists in the project folder and contains a valid key.

### No readable text found
This usually means the PDF is scanned or encrypted. Try using a searchable PDF instead.

### Dependency errors
Reinstall requirements in the active virtual environment:

```bash
pip install -r requirements.txt
```

## License

This project is intended for educational and learning purposes.
