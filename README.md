# AI-Powered Resume Analyzer (Colab - Simple)

A very simple README for running the resume analyzer inside Google Colab. Designed to be minimal so you can run quickly and see results.

What this does
- Parse a resume (PDF / DOCX / TXT)
- Score it and print a small JSON report
- Save a report.json you can download

Quick steps (Colab)

1. Open Google Colab (https://colab.research.google.com).
2. Create a new notebook or upload the project's notebook if you have one.
3. Copy & paste and run the example cells below.

Minimal Colab cells

Install dependencies (run once)
```python
# If you have a requirements.txt in the repo, use it. Otherwise install needed libs directly.
!pip install -q -r requirements.txt || true
# Example installs if you don't have requirements.txt:
!pip install -q python-docx pdfminer.six rapidfuzz
```

Upload files (resume and optional job description)
```python
from google.colab import files
uploaded = files.upload()  # use the UI to upload resume.pdf and optional jd.txt
# Uploaded files will be in /content/
```

Simple analyzer usage (example — adapt to your repo's API)
```python
import json
# Replace with your real analyzer function import
# from resume_analyzer import analyze_resume

# Example placeholder function (delete if you have real code)
def analyze_resume(resume_path, job_description_path=None):
    # Minimal dummy output — replace with real analysis
    return {
        "candidate": {"name": "Unknown"},
        "scores": {"overall": 75},
        "recommendations": ["Use bullet points", "Include metrics"]
    }

# Paths to uploaded files (adjust names as needed)
resume_path = "/content/resume.pdf"    # or resume.docx / resume.txt
jd_path = "/content/jd.txt"            # optional

result = analyze_resume(resume_path, job_description_path=jd_path if jd_path in uploaded else None)
print(json.dumps(result, indent=2))

# Save and download report
with open("report.json", "w") as f:
    json.dump(result, f, indent=2)

files.download("report.json")
```

If you need OpenAI (or other) API keys in Colab
```python
import os
os.environ["OPENAI_API_KEY"] = "sk-..."
# Or use Colab secrets manager / runtime prompt to set securely
```

Notes & tips
- For scanned PDFs you may need OCR (e.g., pytesseract). That increases setup.
- Keep sensitive resumes local if you don't want them sent to external APIs.
- This README is intentionally minimal. If you want, I can:
  - create a full Colab notebook (.ipynb) that runs end-to-end,
  - or provide a one-cell "run everything" script.

License
- MIT
