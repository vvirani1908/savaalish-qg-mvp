# Savaal‑ish Concept‑Driven Question Generation (QG) MVP

Generate **conceptual multiple‑choice questions** from long PDFs/text using a **concept‑driven RAG** pipeline:
extract ideas → retrieve evidence → generate MCQs → score quality → tag difficulty → **export a single JSON**.

> Built for a take‑home assignment; polished for a public showcase.

## 🧭 Why this repo (for reviewers/recruiters)
- Handles **long documents** with token‑aware chunking + retrieval.
- Focuses on **conceptual understanding**, not trivia.
- Clean, modular code with clear **design trade‑offs** documented in the notebook.
- Single JSON output validated by an included **schema**.

## 🚀 Quickstart
```bash
# 0) (Optional) create a venv
python -m venv .venv && source .venv/bin/activate

# 1) Install deps
pip install -r requirements.txt

# 2) Configure secrets (copy and edit)
cp .env.example .env

# 3) Add docs
# Put your PDFs or .txt files into ./docs/

# 4) Run the notebook
# Open Savaalish_QG_MVP.ipynb in Jupyter/VS Code/Colab and run all cells

# Final output:
#   ./output/questions.json
```

## ⚙️ Config
Set these in `.env`:
```
OPENAI_API_KEY=sk-...
OPENAI_MODEL=gpt-4o-mini
OPENAI_EMBEDDING=text-embedding-3-large

MAX_QUESTIONS=20
K_CONTEXT=3
QUALITY_THRESHOLD=0.70
```

## 🧩 Repository layout
```
.
├── Savaalish_QG_MVP.ipynb      # Main notebook (end-to-end pipeline)
├── qg_output_schema.json       # JSON schema for output validation
├── requirements.txt
├── .env.example
├── .gitignore
├── LICENSE
├── README.md
├── docs/                       # (your PDFs/txt go here; .gitkept)
│   └── .gitkeep
└── output/                     # Generated output (JSON); .gitkept
    └── .gitkeep
```

## 🏗️ Architecture (30‑sec view)
```
docs/ (PDF, txt)
   |
   |-- parse & chunk (token-aware windows)
   |         |
   |         `-- map -> combine -> reduce: extract conceptual ideas (LLM)
   |                      |
   |-- embed chunks ------+--> FAISS index
   |                      |
   `-- per-idea retrieve top-k context
                          |
                      question generation (LLM)
                          |
               quality scoring & difficulty (LLM)
                          |
                   output/questions.json
```

## 🧪 Output
- File: `output/questions.json`
- Conforms to: `qg_output_schema.json`
- Each item has: `id, question, choices[A-D], correct_label, idea_summary, source_citations, quality, difficulty`

## 🗺️ Roadmap (nice-to-haves)
- Caching embeddings & LLM calls
- Multi‑doc idea clustering
- Human‑in‑the‑loop editing UI
- Alternative vector DBs & LLM providers
- Cost estimator & token accounting

---

**License:** MIT.  © {year} Vansh Virani
