# FinancialRAG

A Retrieval-Augmented Generation (RAG) application for financial data analysis using DeepSeek LLM, built with Streamlit and powered by LangChain.

## Overview

FinancialRAG is an intelligent document analysis tool that allows you to upload financial PDF documents and ask questions about them using natural language. The application uses advanced RAG techniques to provide accurate, context-aware answers by retrieving relevant information from your documents.

## Features

- 📄 **PDF Document Processing**: Upload and process financial PDF documents using Docling
- 🔍 **Semantic Search**: Uses FAISS vector database for efficient similarity search
- 💬 **Natural Language Q&A**: Ask questions in plain English about your financial documents
- 🖼️ **PDF Preview**: View uploaded PDFs directly in the sidebar
- 💾 **Persistent Storage**: Save processed documents and reuse them without reprocessing
- 🔄 **Streaming Responses**: Real-time answer generation with streaming support
- 🎯 **Context-Aware Answers**: Leverages DeepSeek R1 model for accurate financial analysis

## Prerequisites

Before running this application, you need to have:

1. **Python 3.11+** installed on your system
2. **Poppler** (for PDF to image conversion):
   - **Ubuntu/Debian**: `sudo apt-get install poppler-utils`
   - **macOS**: `brew install poppler`
   - **Windows**: Download from [poppler for Windows](http://blog.alivate.com.au/poppler-windows/)
3. **Ollama** installed and running locally
4. **Required Ollama models**:
   - `nomic-embed-text` (for embeddings)
   - `deepseek-r1:1.5b` (for question answering)

### Installing Ollama and Models

1. Install Ollama from [https://ollama.ai](https://ollama.ai)

2. Pull the required models:
   ```bash
   ollama pull nomic-embed-text
   ollama pull deepseek-r1:1.5b
   ```

3. Ensure Ollama is running:
   ```bash
   ollama serve
   ```

## Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/hyperion912/FinancialRAG.git
   cd FinancialRAG
   ```

2. Install the required Python packages:
   ```bash
   pip install -r requirements.txt
   ```

## Usage

1. Start the Streamlit application:
   ```bash
   streamlit run app.py
   ```

2. Open your browser and navigate to `http://localhost:8501`

3. **Upload a new document**:
   - Select "Upload New Document" from the dropdown
   - Upload a PDF file containing financial data
   - Click "Process PDF and Store in Vector DB"
   - Wait for processing to complete

4. **Query existing documents**:
   - Select a previously processed document from the dropdown
   - Enter your question in the text input field
   - Click "Submit Question" to get an answer

## Project Structure

```
FinancialRAG/
├── app.py                  # Main Streamlit application
├── rag.py                  # RAG pipeline implementation
├── ragbot.ipynb           # Jupyter notebook for experimentation
├── requirements.txt       # Python dependencies
├── vector_db/            # Storage for FAISS vector databases and PDFs
├── .devcontainer/        # Dev container configuration
└── README.md             # This file
```

## How It Works

1. **Document Processing**: PDFs are converted to markdown using Docling
2. **Text Splitting**: Markdown content is split into chunks based on headers
3. **Embedding**: Text chunks are embedded using the `nomic-embed-text` model
4. **Vector Storage**: Embeddings are stored in a FAISS vector database
5. **Retrieval**: When a question is asked, relevant chunks are retrieved using MMR search
6. **Answer Generation**: The DeepSeek model generates answers based on retrieved context

## Configuration

The application uses the following default configurations:

- **Ollama Base URL**: `http://localhost:11434`
- **Embedding Model**: `nomic-embed-text`
- **LLM Model**: `deepseek-r1:1.5b`
- **Vector DB Folder**: `vector_db/`
- **Retrieval Method**: MMR (Maximum Marginal Relevance)
- **Top K Results**: 5

To modify these settings, edit the respective files:
- `app.py` for Streamlit UI settings
- `rag.py` for RAG pipeline configuration

## Dependencies

Core dependencies include:
- `langchain` - LLM orchestration framework
- `langchain-community` - Community integrations
- `langchain-ollama` - Ollama integration
- `faiss-cpu` - Vector similarity search
- `docling` - PDF to markdown conversion
- `streamlit` - Web UI framework
- `pdf2image` - PDF rendering

See `requirements.txt` for the complete list.

## Development

This project includes a dev container configuration for easy development setup. If you're using VS Code or GitHub Codespaces:

1. Open the project in VS Code
2. Click "Reopen in Container" when prompted
3. The environment will be automatically configured

## Troubleshooting

### Ollama Connection Issues
- Ensure Ollama is running: `ollama serve`
- Check if models are installed: `ollama list`
- Verify the base URL in the code matches your Ollama installation

### PDF Processing Errors
- Ensure the PDF is not corrupted
- Check if the PDF contains actual text (not just images)
- Verify you have sufficient disk space for image conversion

### Memory Issues
- Consider using smaller documents
- Reduce the chunk size in `rag.py`
- Use a more lightweight embedding model

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

This project is open source. Please check the repository for license information.

## Acknowledgments

- Built with [LangChain](https://github.com/langchain-ai/langchain)
- Powered by [Ollama](https://ollama.ai) and [DeepSeek](https://github.com/deepseek-ai)
- Document processing by [Docling](https://github.com/DS4SD/docling)
- UI built with [Streamlit](https://streamlit.io)
