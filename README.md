# Conversational RAG With PDF Uploads and Chat History

A conversational Retrieval-Augmented Generation (RAG) app where you upload your own PDFs and chat with their content. Unlike a one-shot Q&A, this app remembers the conversation — so you can ask follow-up questions that refer back to earlier answers, and it understands the context.

## 🔗 Live Demo

**[Launch App](https://conversational-document-q-a-5bzznqjghemfhui42jyt3v.streamlit.app)**

> Enter your Groq API key, upload one or more PDFs, and start asking questions. Bring your own Groq key.

## ✨ Features

- **Upload your own PDFs** — one or several at a time, right from the browser.
- **Conversational memory** — the app keeps chat history per session, so follow-up questions work naturally (e.g. "What about the second one?").
- **History-aware retrieval** — user questions are reformulated into standalone queries using the chat history before retrieval, improving relevance.
- **Session management** — a Session ID field lets you keep separate conversation threads.
- **Free local embeddings** — uses HuggingFace `all-MiniLM-L6-v2`, so no OpenAI key is needed.

## 🔍 How It Works

When you upload PDFs, the app loads and splits them into overlapping chunks, embeds those chunks locally with a HuggingFace model, and stores them in a Chroma vector database. Each question you ask is first passed through a "history-aware retriever" that rewrites it into a self-contained question using the prior conversation, so references like "it" or "that model" are resolved. The rewritten question retrieves the most relevant chunks, which are handed to Groq-hosted Llama 3 to produce a concise answer. Chat history is stored per session in Streamlit's session state, so the context persists across turns.

## 🛠️ Tech Stack

- [Streamlit](https://streamlit.io/) — web UI and file uploads
- [LangChain](https://www.langchain.com/) — history-aware retrieval and RAG chains
- [Groq](https://groq.com/) — fast Llama 3 (`llama-3.1-8b-instant`) inference
- [Chroma](https://www.trychroma.com/) — vector database
- [HuggingFace](https://huggingface.co/) `all-MiniLM-L6-v2` — local text embeddings
- `PyPDFLoader` — PDF loading

## 🚀 Getting Started

### 1. Clone the repo

\`\`\`bash
git clone https://github.com/<your-username>/<your-repo>.git
cd <your-repo>
\`\`\`

### 2. Install dependencies

\`\`\`bash
pip install -r requirements.txt
\`\`\`

If you don't have a \`requirements.txt\` yet, install the core packages:

\`\`\`bash
pip install streamlit langchain langchain-groq langchain-chroma langchain-community langchain-huggingface langchain-text-splitters chromadb pypdf python-dotenv sentence-transformers
\`\`\`

### 3. (Optional) Set up environment variables

The embeddings run locally, so no HuggingFace token is required. If you have one, you can create a \`.env\` file:

\`\`\`
HF_TOKEN=your-huggingface-token
\`\`\`

The **Groq API key is entered directly in the app** at runtime — you don't need to put it in \`.env\`.

### 4. Run the app

\`\`\`bash
streamlit run main.py
\`\`\`

Then enter your Groq API key, upload PDFs, and chat.

## 📝 Notes

- The Groq API key is entered in the app's UI, so each visitor uses their own key — you're not paying for others' usage.
- Embeddings are computed locally with `all-MiniLM-L6-v2`, so the app works without any embedding API key.
- Get a free Groq API key at [console.groq.com](https://console.groq.com).

## 📄 License

This project is open source and available under the [MIT License](LICENSE).
