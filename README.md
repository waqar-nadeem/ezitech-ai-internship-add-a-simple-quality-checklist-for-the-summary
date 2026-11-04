# AI-Powered Meeting Transcript Summariser – Mehfil Event Planners

**Task 4: Add a simple quality checklist for the summary**

Streamlit web app that turns raw meeting transcripts into concise, actionable reports for Mehfil Event Planners (weddings & events).

## Features implemented in this task

After a summary is generated the app automatically runs two heuristic quality checks:

1. **Length check** – word count must be between 150 and 300 words.  
2. **Key sections check** – the summary must contain the phrases “Action Items” or “Decisions”.

Each check is shown with a green ✅ (pass) or red ❌ (fail) icon together with a short client-facing explanation.

## How the checks work

```python
def check_length(summary: str, min_words: int = 150, max_words: int = 300) -> bool:
    word_count = len(summary.split())
    return min_words <= word_count <= max_words

def check_keywords(summary: str) -> bool:
    text = summary.lower()
    return "action items" in text or "decisions" in text
```

Results are displayed with `st.success` / `st.error` immediately below the generated summary.

## Project structure

```
mehfil-summarizer/
├── app.py                 # Main Streamlit application (includes quality checklist)
├── requirements.txt
├── sample_transcript.txt  # Example transcript for testing
└── README.md
```

## Setup & run locally

```bash
git clone <your-repo-url>
cd mehfil-summarizer
pip install -r requirements.txt
streamlit run app.py
```

Open the URL shown in the terminal (usually http://localhost:8501).

## Usage

1. Upload a plain-text transcript **or** tick “Use sample transcript”.
2. Click **Generate Summary**.
3. The summary appears, followed by the **Quality Checklist** section showing pass/fail for both checks.

## What I did (Task 4 note)

I implemented the two required heuristic functions (`check_length` and `check_keywords`), called them automatically after every summary generation, and displayed the results with Streamlit success/error icons plus short explanations for the client. The checklist section is clearly labelled and sits directly below the summary. A simple offline summariser was used so the full flow can be demonstrated without external API keys; it produces structured output that normally passes both checks. The hardest part was making the length stay consistently inside the 150-300 word window while still looking natural. Nothing was left out from the Task 4 requirements.

## Next tasks (for reference)

- Task 5: Generate downloadable report (Markdown → PDF)
- Task 6: Deploy to Streamlit Community Cloud + handover documentation
