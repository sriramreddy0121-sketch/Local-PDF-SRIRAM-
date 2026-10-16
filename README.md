# Local PDF Simplifier

Local PDF Simplifier turns the text in a PDF into simpler notes, a short summary, key points, and explanations of difficult words. It uses the Gemma 3:1B model through Ollama on your computer. The PDF text is not sent to a hosted AI service.

## Features

- Upload text-based PDF files up to 10 MB and 50 pages.
- Extract text with PyMuPDF and simplify it in small chunks.
- Generate a summary, key points, and plain-English word meanings.
- Compare the results with the original extracted text.
- Download the study notes as a `.txt` file.
- Show clear messages for invalid PDFs, scanned PDFs, and Ollama problems.
- Use ordinary HTML forms and navigation; no JavaScript is needed.

## Technologies

- Python and FastAPI for the web server and PDF upload.
- PyMuPDF for reading PDF text.
- Ollama with the local `gemma3:1b` model for text simplification.
- HTML templates and external CSS for the website.

## Project files

```text
LocalPDF-Simplifier/
├── main.py
├── requirements.txt
├── README.md
├── .gitignore
├── LICENSE
├── static/
│   └── style.css
└── templates/
    ├── index.html
    └── results.html
```

## Install on Windows

Install Python 3.10 or later and [Ollama for Windows](https://ollama.com/download). Open this project folder in VS Code, then open **Terminal > New Terminal** and run these PowerShell commands:

```powershell
py -m venv .venv
.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
pip install -r requirements.txt
```

If PowerShell blocks virtual environment activation, allow it for this terminal session and activate again:

```powershell
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
.venv\Scripts\Activate.ps1
```

## Start Ollama and download Gemma

Open a terminal and download the model:

```powershell
ollama pull gemma3:1b
```

Ollama usually starts its local service when installed. To check the model and start an interactive session, run:

```powershell
ollama run gemma3:1b
```

Keep Ollama running while you use the website. If Ollama is not running as a background service, start it in a separate terminal with `ollama serve`. If you see a message that port 11434 is already in use, Ollama is already running; do not start a second copy.

## Run the website in VS Code

In the project folder, with `.venv` activated, start FastAPI:

```powershell
python -m uvicorn main:app --reload
```

Open <http://127.0.0.1:8000> in your browser. Keep this terminal open while testing. Press `Ctrl+C` in it to stop the web server.

## Use the application

1. Confirm Ollama is running and `gemma3:1b` is installed.
2. Open the website and choose a text-based PDF no larger than 10 MB or 50 pages.
3. Select **Simplify my PDF** and wait while Gemma creates the study material.
4. Use the links at the top of the results to jump to notes, summary, key points, word explanations, or original text.
5. Select **Download study notes (.txt)** to save a text file.

### Test with a sample PDF

Create a short document in Word or another document editor with a few paragraphs, for example a paragraph from a class lesson. Save or export it as a PDF, then upload that PDF to the website. Confirm the results page shows all five sections and that the download button saves `simplified-notes.txt`. Avoid private documents when testing or publishing examples.

## Current limitations

- Scanned PDFs that contain images instead of selectable text need OCR; OCR is not included.
- The model can make mistakes. Check important details against the original text.
- Processing time depends on the computer and document size. Ollama and Gemma need enough memory to run locally.
- Very long PDFs can take several minutes because their content is processed in chunks.
- The app is intended for local use and does not include user accounts, cloud storage, or multi-user security features.

## Push to GitHub

Create an empty repository on GitHub first. In PowerShell, from the project folder, run these commands and replace the repository URL with your own:

```powershell
git init
git add main.py templates/index.html templates/results.html static/style.css requirements.txt README.md .gitignore LICENSE
git commit -m "Build Local PDF Simplifier"
git branch -M main
git remote add origin https://github.com/YOUR-USERNAME/LocalPDF-Simplifier.git
git push -u origin main
```

The `.gitignore` excludes virtual environments, local PDFs, environment variables, and Python cache files. Do not force-add private documents or secrets.