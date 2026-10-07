# 📄 ATS Resume Checker

Upload a resume (PDF, DOCX or TXT) and get an estimated **ATS score**, a score
breakdown, strengths, missing keywords, and prioritized improvements. You can
optionally paste a job description to get keyword matching against a specific role.

Built with [Streamlit](https://streamlit.io) and the Google Gemini Flash model.

> **Note:** The score is an AI estimate of ATS readiness. It is not the output of
> any real ATS, and different systems behave differently. Use it as guidance.

## Features

- Reads PDF, DOCX and TXT resumes
- Overall ATS score (0-100) plus 5 category scores
- Prioritized improvements with example rewrites
- Missing keywords, optionally matched to a job description
- Downloadable JSON report

## Run locally

1. Get a free API key from [Google AI Studio](https://aistudio.google.com/apikey).
2. Install and run:

```bash
python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate
pip install -r requirements.txt
```

3. Provide your key (pick one):

```bash
# Option A: environment variable
export GEMINI_API_KEY="your-key"          # Windows PowerShell: $env:GEMINI_API_KEY="your-key"

# Option B: Streamlit secrets file (create .streamlit/secrets.toml)
GEMINI_API_KEY = "your-key"
```

   If you set neither, the app shows a key box in the sidebar.

4. Start the app:

```bash
streamlit run app.py
```

## Configuration

| Setting | Where | Default |
|---|---|---|
| `GEMINI_API_KEY` | env var or Streamlit secrets | none (required) |
| `GEMINI_MODEL` | env var or Streamlit secrets | `gemini-2.5-flash` |

If Google retires or renames the model, set `GEMINI_MODEL` to a current Flash model name.

## Deploy on Streamlit Community Cloud

1. Push this folder to a GitHub repository.
2. Go to [share.streamlit.io](https://share.streamlit.io) and sign in with GitHub.
3. Click **Create app**, pick your repo, branch `main`, and main file `app.py`.
4. Open **Advanced settings → Secrets** and add:
   ```toml
   GEMINI_API_KEY = "your-key"
   ```
5. Click **Deploy**.

Never commit your API key. `.gitignore` already excludes `.streamlit/secrets.toml` and `.env`.

## Privacy

Resume text is sent to Google's Gemini API for analysis. Do not upload anything
you are not comfortable sharing.

## Limitations

- Scanned/image-only PDFs have no extractable text and are rejected (real ATS tools struggle with them too).
- Only the first ~20,000 characters of a resume are analyzed.
- AI output can be imperfect; review suggestions before applying them.
