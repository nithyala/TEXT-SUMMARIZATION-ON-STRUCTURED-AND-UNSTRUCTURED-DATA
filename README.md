# LangChain: Summarize Text From YouTube or Website

A Streamlit app that generates a concise summary of any **YouTube video** or **website** — just paste a URL and get a ~300-word summary powered by **Groq**-hosted **Llama 3**.

## 🔗 Live Demo

**[Launch App](https://text-summarization-on-structured-and-unstructured-data-7jhwrm6.streamlit.app)**

> Enter your Groq API key in the sidebar, paste a YouTube or website URL, and click summarize. Bring your own Groq key.

## ✨ Features

- **Summarize YouTube videos** — pulls the video transcript and summarizes it.
- **Summarize any website** — loads the page content and condenses it.
- **URL validation** — checks the input is a valid URL before processing.
- **One-click summaries** — paste, click, done.
- Powered by fast Groq inference for near-instant results.

## 📂 Project Files

| File | Description |
|------|-------------|
| `main.py` | The Streamlit web app — the deployed summarizer for YouTube and website URLs. |
| `text_summarization.ipynb` | A learning notebook walking through summarization techniques in LangChain: direct chat-message summaries, prompt templates with translation, the **stuff** chain, **map-reduce** for large documents, and the **refine** chain. |

## 🔍 How It Works

When you submit a URL, the app first validates it. If it's a YouTube link, it uses a YouTube loader to fetch the transcript; otherwise it uses an unstructured URL loader (with a browser user-agent) to pull the page's text. The loaded content is then passed to a LangChain "stuff" summarization chain with a custom prompt, and Groq-hosted Llama 3 produces the final ~300-word summary.

The companion notebook goes deeper into the different summarization strategies, which matter depending on document size: the **stuff** chain sends everything at once (simple, but limited by context length), **map-reduce** summarizes chunks separately then combines them (good for long documents), and **refine** builds the summary iteratively chunk by chunk.

## 🛠️ Tech Stack

- [Streamlit](https://streamlit.io/) — web UI
- [LangChain](https://www.langchain.com/) — summarization chains and document loaders
- [Groq](https://groq.com/) — fast Llama 3 (`llama-3.1-8b-instant`) inference
- `YoutubeLoader` — fetches YouTube transcripts
- `UnstructuredURLLoader` — loads website content
- `validators` — URL validation

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
pip install streamlit langchain langchain-groq langchain-community validators youtube-transcript-api unstructured python-dotenv
\`\`\`

### 3. Run the app

\`\`\`bash
streamlit run main.py
\`\`\`

Then enter your Groq API key in the sidebar and paste a URL.

## 📝 Notes

- The Groq API key is entered in the app at runtime, so each visitor uses their own key.
- Get a free Groq API key at [console.groq.com](https://console.groq.com).
- Some websites block automated loaders, and some YouTube videos have transcripts disabled — those URLs may not summarize.


