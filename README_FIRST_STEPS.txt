
Savaal-ish QG MVP - Quick Steps
================================
1) Create a new folder and copy the notebook:
   - /mnt/data/qg_mvp/Savaalish_QG_MVP.ipynb

2) In the same folder, create a "docs" directory and drop your PDFs or .txt files inside:
   - ./docs/yourfile.pdf

3) Install Python 3.10+ and run the notebook (VS Code, Jupyter, or Colab).

4) Export your LLM credentials in your shell (example for OpenAI):
   export OPENAI_API_KEY=sk-...

5) Run the notebook top to bottom. The final JSON appears at:
   ./output/questions.json

6) Zip your deliverables:
   - the .ipynb notebook
   - output/questions.json
   - (optional) a short screen recording showing a run + final JSON.

Tips:
- Use MAX_QUESTIONS env var to control size (default 20)
- For long documents, consider lowering chunk max tokens to ~700 and overlap to 120.
- If FAISS install has issues on your platform, consider 'pip install faiss-cpu' or use a simple cosine search in NumPy as a fallback.
