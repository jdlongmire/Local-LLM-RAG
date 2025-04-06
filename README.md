🚀 Local LLM with RAG & Web UI
Welcome to LocalLLM-RAG, a slick, self-hosted AI chat system running on Windows! Upload your docs (.txt or .pdf), ask questions, and get answers powered by a local LLM with Retrieval-Augmented Generation (RAG)—no internet needed after setup. Built with grit, Python, and a dash of Rust, this project’s ready to roll.
🌟 Features
Local AI: Runs phi-3 (3.8B params) via Ollama—fast and offline.
RAG Magic: Indexes your docs into ChromaDB for context-aware answers.
Web UI: Flask-powered interface at localhost:5000 with file uploads.
Performance: Optimized for CPU, with timing stats to keep it snappy.
🏛️ System Architecture
Overview
A lightweight, local LLM setup with RAG, all on your Windows box. Upload docs, query away, and watch it shine—all without cloud dependency.
Components
Layer
Tech
Purpose
Hardware
Windows PC (8GB+ RAM)
Runs everything, CPU-based (GPU optional)
OS
Windows 10/11
Hosts the stack
Runtime
Python 3.12.7, Rust
Core execution, tokenizers build
LLM Server
Ollama (phi-3)
Generates responses
Web Framework
Flask
Serves UI at localhost:5000
Vector DB
ChromaDB
Stores RAG embeddings
Embedding Engine
Sentence Transformers
Turns text into vectors
PDF Parser
PyPDF2
Extracts text from PDFs
Setup Script
PowerShell (setup_llm.ps1)
Automates install
Dependencies
Pinned for stability:
numpy==1.26.4
transformers==4.44.2 (needs Rust!)
accelerate==0.34.2
sentence-transformers==3.2.0
flask, chromadb, ollama, PyPDF2
File Structure
C:\MyLLM\
├── app.py           # Flask app with UI & RAG
├── data\           # Upload your .txt/.pdf here
├── chroma_db\      # ChromaDB embeddings
├── setup_log.txt   # Setup logs
└── README.txt      # Usage guide
Data Flow
Setup: setup_llm.ps1 installs Python 3.12, Rust, Ollama, and deps. Pulls phi-3.
Startup: app.py loads all-MiniLM-L6-v2, indexes data/ (~30s), starts Flask.
Query:
Upload: Saves to data/, re-indexes.
Ask: Embeds query, searches ChromaDB, generates with phi-3 (~2-10s).
Output: UI shows answer + timing.
Diagram
[You] --> [Browser: localhost:5000]
   |
[Flask: app.py]
   |--> [Upload: C:\MyLLM\data]
   |--> [Query]
         |--> [Sentence Transformers]
         |     |--> [tokenizers: Rust]
         |--> [ChromaDB]
         |--> [Ollama: phi-3]
[Response] <-- [UI]
⚙️ Setup Instructions
Prerequisites
Windows 10/11
8GB+ RAM (16GB+ for speed)
Internet (for initial downloads)
Steps
Install Python 3.12.7:
Download from python.org (64-bit).
Check “Add to PATH” during install.
Verify: python --version → Python 3.12.7.
Install Rust:
Get rustup-init.exe from rustup.rs.
Run it, accept defaults.
Verify: rustc --version (e.g., 1.81.0).
Clone & Run Setup:
powershell
git clone <your-repo-url>
cd LocalLLM-RAG
.\setup_llm.ps1
Follow prompts: Use C:\MyLLM, pick “1” (internet mode).
Installs Ollama, pulls phi-3, sets up deps.
Start the App:
powershell
python C:\MyLLM\app.py
Open http://localhost:5000 in your browser.
Use It:
Upload: Drop a .txt or .pdf via the UI.
Query: Ask something (e.g., “Summarize this”).
🎯 Usage
Upload: Add files to C:\MyLLM\data via UI. Re-indexes in ~30s.
Query: Type a question, get a response in 2-10s (CPU-dependent).
Debug: Check timing in UI (e.g., “Total: 5.2s, Query: 0.1s, Generate: 5.1s”).
🔧 Lessons Learned
Python 3.13 Flop: Too new—PyO3 in tokenizers capped at 3.12.
Rust Required: tokenizers needs it for speed (no prebuilt wheels).
Model Swap: llama3 (7B) → phi-3 (3.8B) for faster CPU inference.
Indexing Fix: Moved to startup/upload, not per-query.
Context Cap: Limited to 1000 chars to speed up generation.
🚀 Performance Tips
Smaller Model: Try gemma:2b (ollama pull gemma:2b) for even faster responses.
GPU Boost: Add NVIDIA GPU + CUDA for <5s queries.
Slim Data: Keep data/ lean—fewer/big files slow indexing.
🤝 Contributing
Fork it, tweak it, PR it! Issues welcome—let’s make it faster.
📜 Credits
Built with ❤️ by [Your Name] & Grok 3 (xAI). Shoutout to the Rust, Python, and Ollama crews!
Files to Include
setup_llm.ps1: Your latest PowerShell script.
app.py: The latest Flask app with upload and phi-3.
This README’s got swagger and substance—your tech buddies will dig it! Want to tweak anything (e.g., your name, repo details) before pushing to GitHub? What’s your latest query time with phi-3?
