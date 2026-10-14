# 📄 AI Resume ATS Checker

Upload a resume (PDF, DOCX or TXT), optionally paste a job description, and get:

- an **ATS score out of 100** with a weighted category breakdown
- your **strengths** and **missing keywords**
- **prioritized improvements** (high / medium / low)
- **suggested rewrites** for weak bullet points

Built with [Streamlit](https://streamlit.io) and Google's Gemini Flash model.

## How the score works

Gemini rates five categories from 0 to 100. The overall score is calculated in code as a weighted average, so it is consistent and explainable:

| Category | Weight |
|---|---|
| Keywords & Relevance | 25% |
| Impact & Achievements | 25% |
| Formatting & Structure | 20% |
| Skills Presentation | 15% |
| Clarity & Grammar | 15% |

> This is an AI estimate, not the output of a real employer's ATS. Use it as guidance.

## Run locally

1. Get a free API key from [Google AI Studio](https://aistudio.google.com/apikey).
2. Install and run:

```bash
python -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate
pip install -r requirements.txt
export GEMINI_API_KEY="your-key" # Windows PowerShell: $env:GEMINI_API_KEY="your-key"
streamlit run app.py
```

You can also skip the environment variable and paste the key into the app's sidebar.

### Optional settings

- `GEMINI_MODEL` - override the model (default `gemini-2.5-flash`). You can also change it in the sidebar.

## Deploy on Streamlit Community Cloud (free)

1. Push this project to a GitHub repository (see below).
2. Go to [share.streamlit.io](https://share.streamlit.io) and sign in with GitHub.
3. Click **Create app**, choose your repo, branch `main`, and main file `app.py`.
4. Open **Advanced settings → Secrets** and add:
   ```toml
   GEMINI_API_KEY = "your-key"
   ```
5. Click **Deploy**. You get a public URL like `https://your-app.streamlit.app`.

## Push to GitHub

Create a `.gitignore` first so secrets never get committed:

```
venv/
__pycache__/
.env
.streamlit/secrets.toml
```

Then:

```bash
git init
git add app.py requirements.txt README.md .gitignore
git commit -m "Initial commit: AI Resume ATS Checker"
git branch -M main
git remote add origin https://github.com/<your-username>/<repo-name>.git
git push -u origin main
```

(Create the empty repo on github.com first, without a README, then use its URL above.)

## Privacy

Resume text is sent to the Gemini API for analysis. The app itself does not store uploaded files or results.

## Project structure

```
app.py            # Streamlit app
requirements.txt  # Python dependencies
README.md
```
