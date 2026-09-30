# LangChain, RAG & Agentic AI — Two-Day Hands-On Workshop

*Created by Prashant Sahu · [LinkedIn](https://www.linkedin.com/in/prashantksahu/)*

This repository holds the **Day 1** materials: four modules, seven session labs, three take-home labs and the
slide decks. Every notebook has been run top to bottom on the exact versions in `requirements.txt`. The outputs
under its cells come from that run, apart from the few cells listed under
[Cells without a fresh output](#cells-without-a-fresh-output).

## What is in Day 1

| Module | Session labs | Take-home |
|---|---|---|
| 1 · Prompt Engineering & Structured Outputs | 1.1 Prompting Techniques & Structured Outputs | Prompt Caching · Multi-Modal Prompt Engineering Workflow |
| 2 · LangChain Deep Dive & LLM Reliability | 2.1 LangChain Fundamentals · 2.2 LLM Robustness: Retries, Fallback & Hallucination Signals | |
| 3 · RAG Foundations | 3.1 Document Loaders & Chunking · 3.2 Embeddings & Semantic Search | |
| 4 · Production RAG | 4.1 End-to-End RAG with LCEL & Citations · 4.2 Conversational RAG | Advanced Retrieval Strategies |

The slide decks sit at the top of the `Day 1` folder, numbered in teaching order. Each is a single HTML file,
so open it in any browser:

1. GenAI Fundamentals — A Beginner's Guide
2. Fundamentals of Prompt Engineering — Banking Domain
3. RAG Systems Part 1: Embeddings & Vector Databases
4. RAG Systems Part 2: Architecture, Frameworks, Evaluation & Advanced Techniques

One more deck sits at the top of the repository: *AI Fundamentals & Applications in Banking*
(`ai-fundamentals-banking-presentation.html`).

Data files sit **beside the notebook that reads them**:
- `Module 3 - RAG Foundations/` — a sample Markdown file (`langchain_readme_sample.md`) and two PDFs.
- `Module 4 - Production RAG/docs/` — nine banking-policy documents.
- `Module 4 - Production RAG/Take-Home/rag_docs/` — research papers and a Wikipedia extract.

Leave them where they are.

```
Day 1/
├── 1. genai-fundamentals-presentation.html …         slide decks
├── Module 1 - Prompt Engineering & Structured Outputs/
│   ├── Lab_1.1_….ipynb
│   └── Take-Home/  Prompt_Caching.ipynb · Multimodal_Prompt_Engineering_Workflow.ipynb
├── Module 2 - LangChain Deep Dive & LLM Reliability/   Lab_2.1_….ipynb · Lab_2.2_….ipynb
├── Module 3 - RAG Foundations/                          Lab_3.1_….ipynb · Lab_3.2_….ipynb · sample files
└── Module 4 - Production RAG/                           Lab_4.1_….ipynb · Lab_4.2_….ipynb · docs/
    └── Take-Home/  Advanced_Retrieval_Strategies.ipynb · rag_docs/
```

## Getting started

**On the workshop VM** everything is already installed. Open the workshop folder in Jupyter or VS Code, select
the workshop's Python kernel, and go straight to [Keys](#keys--what-you-need-and-when).

**On your own machine,** use Python 3.12:

```bash
git clone https://github.com/prashant9501/SCB_Training.git
cd SCB_Training
python -m venv .venv
.venv\Scripts\activate          # macOS / Linux: source .venv/bin/activate
pip install -r requirements.txt
```

On Windows, clone into a short path such as `C:\workshop`. A few file paths in this repository are long, and
Git for Windows refuses paths over 260 characters unless long paths are on
(`git config --global core.longpaths true`).

Open each notebook from its own folder. The labs read their data with paths relative to the notebook, which
Jupyter and VS Code use as the working directory by default.

## Keys — what you need, and when

Keys go into a `.env` file at the top of this folder, one `KEY_NAME=value` per line. Copy `.env.example` to
`.env` to start. Every lab's key cell tells you which key is missing and where to get it. `.env` is excluded
by `.gitignore`: never paste a key into a notebook cell, and never commit `.env`.

| Needed from | Key | Where | Used by |
|---|---|---|---|
| Module 1 | `OPENAI_API_KEY` | supplied by the trainer on the workshop VM; otherwise platform.openai.com/api-keys | every lab |
| Module 2 | `GROQ_API_KEY` | console.groq.com/keys | 2.1, 2.2 |
| Module 2 | `LANGSMITH_API_KEY` | smith.langchain.com → Settings → API Keys | 2.2 |
| Take-home labs | `ANTHROPIC_API_KEY` | console.anthropic.com/settings/keys | Prompt Caching, Advanced Retrieval |
| Take-home labs | `GEMINI_API_KEY` | aistudio.google.com/app/apikey | Prompt Caching |

Groq, LangSmith and Gemini have free tiers; OpenAI and Anthropic bill per use. `.env.example` also lists two
keys that only the Day 2 labs use; leave them empty for now.

## How each lab is laid out

- A **run-list** under the title says which sections run **live in the session** and which are for **after the
  session**. After-session sections are marked ⏭️ and kept in full, so you can finish them at your own pace.
- Every notebook's set-up has the same two cells:
  - a package report (the install line is commented out, because the VM has everything);
  - `load_keys(...)`, which stops with instructions if a key the lab needs is missing.
- Some labs write working files when they run (a FAISS index, a Chroma store, a saved conversation). They are
  recreated on every run, so deleting them is always safe, and `.gitignore` keeps them out of commits.

**One expected warning.** Several RAG labs import from `langchain-community`, which LangChain stopped
maintaining in May 2026. The loaders and vector stores used from it have no maintained replacement yet, so the
workshop pins the tested version. The first import prints a `DeprecationWarning`, and the code works as shown.
Each affected lab explains this in a note under its package report.

## Cells without a fresh output

A few cells need something the machine that ran the notebooks did not have:

| Cells | They need | What the notebook shows |
|---|---|---|
| Lab 3.1 — the two `hi_res` PDF cells (after the session) | Tesseract OCR and Poppler, on PATH (installed on the VM) | No output until you run them |
| Multi-Modal take-home — the video steps, and the cells built on a video | Access to a paid video model (Sora) | The original course run's output where it had one, otherwise none |

The Multi-Modal take-home also writes its generated images and audio beside the notebook. `.gitignore` keeps
those files out of commits too.

## Running on Colab

Each notebook's commented-out `!pip install` line installs what it needs, and its key cell reads keys from the
🔑 Secrets panel instead of a `.env` file. The labs read their data from their own folder, so clone the
repository inside Colab and start from the module folder:

```python
!git clone https://github.com/prashant9501/SCB_Training.git
%cd "SCB_Training/Day 1/Module 4 - Production RAG"
```
