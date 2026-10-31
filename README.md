# Simple RAG Application with LangChain, FAISS and Groq

A beginner-friendly Retrieval-Augmented Generation (RAG) application built with Python, LangChain, Hugging Face embeddings, FAISS and Groq.

This project demonstrates the basic RAG pipeline:

```text
User Question
      ↓
Question Embedding
      ↓
FAISS Similarity Search
      ↓
Relevant Document Chunks
      ↓
Retrieved Context
      ↓
Groq LLM
      ↓
Grounded Answer
```

The purpose of this project is to help learners understand the fundamental building blocks of a RAG application before moving to more advanced frameworks and production architectures.

---

## 1. What This Application Does

The application contains a small set of insurance and banking-related information.

For example:

- Customers can cancel their insurance policy within 14 days of purchase.
- Customers should contact the bank immediately if their banking credentials are exposed.
- The bank may temporarily hold a suspicious transaction while verification is completed.
- Complaints can be raised through customer support, online banking, or a branch.
- The bank aims to provide a final response to standard complaints within 15 business days.

The application converts this information into embeddings, stores those embeddings in a FAISS vector store, retrieves relevant chunks for each user question, and sends only the retrieved context to the Groq LLM.

---

# 2. Technology Stack

| Technology | Purpose |
|---|---|
| Python 3.12.x | Programming language |
| VS Code | Development environment |
| LangChain | RAG orchestration |
| Hugging Face | Embedding model |
| Sentence Transformers | Generates embeddings |
| FAISS | Local vector store |
| Groq | LLM inference |
| python-dotenv | Environment variable management |

---

# 3. Prerequisites

Before starting, install:

1. Git
2. Python 3.12.x
3. Visual Studio Code
4. VS Code Python extension
5. A Groq account
6. A Groq API key

You do not need:

- Anaconda
- Docker
- Kubernetes
- A database server
- A cloud account
- A GPU

This project uses FAISS locally and a hosted Groq LLM.

---

# 4. Install Git

## Windows

Download Git from:

https://git-scm.com/downloads

After installation, open PowerShell or Git Bash and verify:

```bash
git --version
```

You should see something similar to:

```text
git version 2.x.x
```

## macOS

If Git is already installed:

```bash
git --version
```

If macOS asks you to install Command Line Tools, accept the installation.

---

# 5. Install Python 3.12

Python 3.12.x is recommended for this project.

Python 3.12.5 is the version used while developing/testing this training material.

Download Python from the official Python website:

https://www.python.org/downloads/

Python 3.12.5:
https://www.python.org/downloads/release/python-3125/

---

## Windows Installation

Download the Windows installer.

During installation:

### IMPORTANT

Enable:

```text
Add python.exe to PATH
```

Then select:

```text
Install Now
```

After installation, open a **new** PowerShell window.

Verify:

```powershell
python --version
```

Expected:

```text
Python 3.12.x
```

Also verify pip:

```powershell
python -m pip --version
```

If `python` is not recognized, try:

```powershell
py --version
```

If `py` works but `python` does not, Python may not have been added to PATH.

---

## macOS Installation

Install Python 3.12 from the official Python website.

Open Terminal and verify:

```bash
python3 --version
```

Expected:

```text
Python 3.12.x
```

Verify pip:

```bash
python3 -m pip --version
```

> Note: macOS commonly uses `python3` instead of `python`.

---

# 6. Install Visual Studio Code

Download Visual Studio Code:

https://code.visualstudio.com/

Install VS Code using the default installation options.

VS Code's Python setup requires three separate pieces:

1. VS Code
2. Python interpreter
3. Python extension

---

# 7. Install the Python Extension in VS Code

Open VS Code.

Go to:

```text
Extensions
```

Search for:

```text
Python
```

Install:

```text
Python
Publisher: Microsoft
```

The official VS Code Python documentation recommends installing VS Code, an actively supported Python interpreter, and the Microsoft Python extension. 

---

# 8. Clone the Repository

Open a terminal.

Navigate to the location where you want to store the project.

Example:

```bash
cd Documents
```

Clone the repository:

```bash
git clone <YOUR_GITHUB_REPOSITORY_URL>
```

Example:

```bash
git clone https://github.com/<username>/simple-rag.git
```

Move into the project:

```bash
cd simple-rag
```

---

# 9. Open the Project in VS Code

From the project directory:

```bash
code .
```

If the `code` command is not available, open VS Code manually and select:

```text
File → Open Folder
```

Select the `simple-rag` folder.

---

# 10. Create a Python Virtual Environment

A virtual environment keeps this project's Python packages isolated from other projects on your machine.

This is strongly recommended.

---

## Windows

Open the VS Code terminal.

PowerShell:

```powershell
python -m venv .venv
```

Activate it:

```powershell
.venv\Scripts\Activate.ps1
```

You should see:

```text
(.venv)
```

at the beginning of your terminal prompt.

### If PowerShell blocks activation

You may see an execution-policy error.

Use:

```powershell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```

Then activate again:

```powershell
.venv\Scripts\Activate.ps1
```

Alternatively, use Command Prompt:

```cmd
.venv\Scripts\activate.bat
```

---

## macOS

Create the virtual environment:

```bash
python3 -m venv .venv
```

Activate:

```bash
source .venv/bin/activate
```

You should see:

```text
(.venv)
```

at the beginning of the terminal prompt.

---

# 11. Select the Python Interpreter in VS Code

In VS Code:

```text
Ctrl + Shift + P
```

Windows/Linux

or:

```text
Cmd + Shift + P
```

macOS

Search for:

```text
Python: Select Interpreter
```

Select the interpreter inside:

```text
.venv
```

For example:

Windows:

```text
.venv\Scripts\python.exe
```

macOS:

```text
.venv/bin/python
```

This is an important step.

Make sure VS Code is using the `.venv` interpreter and not another Python installation.

---

# 12. Upgrade pip

With the virtual environment activated:

Windows:

```powershell
python -m pip install --upgrade pip
```

macOS:

```bash
python3 -m pip install --upgrade pip
```

If your virtual environment is active, you can normally use:

```bash
python -m pip install --upgrade pip
```

on both platforms.

---

# 13. Install Project Dependencies

Make sure you are inside the project directory.

Run:

```bash
pip install -r requirements.txt
```

This installs all required libraries.

The installation may take several minutes because the Hugging Face embedding stack downloads additional machine-learning dependencies.

---

# 14. Verify the Installation

Run:

```bash
pip list
```

You should see packages including:

```text
langchain-core
langchain-community
langchain-text-splitters
langchain-huggingface
langchain-groq
sentence-transformers
faiss-cpu
python-dotenv
```

You can also verify Python:

```bash
python --version
```

---

# 15. Create a Groq Account

The application uses Groq for LLM inference.

Go to:

https://console.groq.com/

Sign in or create a Groq account.

---

# 16. Create a Groq API Key

After signing into Groq Console:

1. Open the Groq Console.
2. Go to the API Keys section.
3. Create a new API key.
4. Give the key a meaningful name, for example:

```text
simple-rag-learning
```

5. Copy the generated API key.

### IMPORTANT

Treat your API key like a password.

Do NOT:

- Put it directly in Python code.
- Commit it to Git.
- Push it to GitHub.
- Share it in screenshots.
- Send it through chat/email.

---

# 17. Create the `.env` File

In the root of the project, create:

```text
.env
```

Add:

```text
GROQ_API_KEY=your_actual_groq_api_key
GROQ_MODEL=openai/gpt-oss-120b
```

For example:

```text
GROQ_API_KEY=gsk_xxxxxxxxxxxxxxxxx
GROQ_MODEL=openai/gpt-oss-120b
```

Do not include quotes unless your key requires them.

---

# 18. Why We Use `.env`

The application contains:

```python
from dotenv import load_dotenv

load_dotenv()
```

This loads environment variables from `.env`.

The application then reads:

```python
os.getenv("GROQ_API_KEY")
```

and:

```python
os.getenv("GROQ_MODEL")
```

This keeps secrets and configuration outside the Python source code.

---

# 19. Verify `.gitignore`

Make sure your `.gitignore` contains:

```text
.env
.venv/
```

Run:

```bash
git status
```

You should NOT see `.env` listed as a file ready to commit.

---

# 20. Run the Application

Make sure the virtual environment is activated.

Windows:

```powershell
.venv\Scripts\Activate.ps1
```

macOS:

```bash
source .venv/bin/activate
```

Then run:

```bash
python simple_rag.py
```

---

# 21. First Run

The application will create the embedding model.

The first execution may take longer because the Hugging Face model:

```text
sentence-transformers/all-MiniLM-L6-v2
```

needs to be downloaded.

After that, you should see something similar to:

```text
Created 3 chunks.

Vector store created.
```

The exact number of chunks may vary if the source text or chunk configuration changes.

You will then see:

```text
Ask a question (or type 'exit'):
```

---

# 22. Try These Questions

Try:

```text
How long do customers have to cancel an insurance policy?
```

Expected answer should be based on the supplied information:

```text
Customers can cancel their insurance policy within 14 days of purchase.
```

Try:

```text
What should I do if my banking credentials are exposed?
```

Try:

```text
How can I raise a complaint?
```

Try:

```text
How long does the bank aim to take to respond to standard complaints?
```

Try a question that is not present:

```text
What is the interest rate for savings accounts?
```

The application should respond:

```text
I could not find that information.
```

This demonstrates the basic grounding behavior implemented in the prompt.

---

# 23. Exit the Application

Type:

```text
exit
```

and press Enter.

---

# 24. Understanding the RAG Pipeline

The application follows these steps.

### Step 1 — Source Data

The application starts with a piece of text:

```python
text = """
Customers can cancel their insurance policy within 14 days of purchase.
...
"""
```

---

### Step 2 — Create a Document

LangChain converts the text into a `Document`:

```python
document = Document(page_content=text)
```

---

### Step 3 — Chunking

The document is split into smaller pieces:

```python
RecursiveCharacterTextSplitter(
    chunk_size=200,
    chunk_overlap=20
)
```

Chunking makes it possible to retrieve smaller relevant pieces instead of sending the entire document to the LLM.

---

### Step 4 — Embeddings

The application uses:

```text
sentence-transformers/all-MiniLM-L6-v2
```

to convert text into numerical vectors.

Conceptually:

```text
Text
 ↓
Embedding Model
 ↓
[0.12, -0.43, 0.78, ...]
```

---

### Step 5 — Vector Store

FAISS stores the vectors:

```python
vectorstore = FAISS.from_documents(
    chunks,
    embeddings
)
```

FAISS enables similarity-based retrieval.

---

### Step 6 — User Question

The user enters:

```text
How long can I cancel my insurance policy?
```

The question is also converted into an embedding.

---

### Step 7 — Similarity Search

The application searches FAISS:

```python
results = vectorstore.similarity_search(
    question,
    k=2
)
```

The two most relevant chunks are retrieved.

---

### Step 8 — Build Context

The retrieved chunks are combined:

```python
context = "\n".join(
    document.page_content
    for document in results
)
```

---

### Step 9 — Send Context to the LLM

The prompt instructs the LLM:

```text
Answer the question using ONLY the information provided below.
```

The retrieved context is included in the prompt.

---

### Step 10 — Generate Answer

Groq generates the final response.

The important concept is:

```text
LLM does not directly search the document.

Retriever finds relevant information.
       ↓
Relevant information is placed into the prompt.
       ↓
LLM generates the answer using that context.
```

This is the fundamental idea behind Retrieval-Augmented Generation.

---

# 25. Common Problems and Solutions

## Problem 1 — `python` command not found

### Windows

Try:

```powershell
py --version
```

If this works, Python is installed but may not be configured correctly in PATH.

Restart the terminal after installing Python.

---

### macOS

Try:

```bash
python3 --version
```

macOS commonly uses `python3`.

---

# Problem 2 — `pip` command not found

Instead of:

```bash
pip install -r requirements.txt
```

use:

```bash
python -m pip install -r requirements.txt
```

On macOS:

```bash
python3 -m pip install -r requirements.txt
```

---

# Problem 3 — VS Code uses the wrong Python interpreter

Use:

```text
Command Palette
→ Python: Select Interpreter
→ Select .venv
```

Then open a new terminal.

---

# Problem 4 — `GROQ_API_KEY` error

Make sure:

```text
.env
```

exists in the project root.

Example:

```text
simple-rag/
├── simple_rag.py
├── requirements.txt
├── .env
└── .gitignore
```

And `.env` contains:

```text
GROQ_API_KEY=your_actual_key
```

---

# Problem 5 — Groq model error

Groq periodically changes its available models.

Check the current model list in Groq Console:

https://console.groq.com/docs/models

Then update:

```text
GROQ_MODEL=...
```

in `.env`.

---

# Problem 6 — FAISS installation problem

First upgrade pip:

```bash
python -m pip install --upgrade pip
```

Then:

```bash
pip install faiss-cpu
```

If that succeeds, run:

```bash
pip install -r requirements.txt
```

---

# Problem 7 — Hugging Face model download takes time

The first execution downloads:

```text
sentence-transformers/all-MiniLM-L6-v2
```

This is normal.

You need an internet connection during the first model download.

Subsequent runs can reuse the locally cached model.

---

# Problem 8 — SSL / corporate network issues

If you are working from a corporate machine, firewall/proxy restrictions may prevent:

- PyPI downloads
- Hugging Face model downloads
- Groq API calls

If this happens, check with your organization's network/security team rather than disabling security controls.

---

# 26. Project Files

```text
simple-rag/
│
├── simple_rag.py
│   └── Main RAG application
│
├── requirements.txt
│   └── Python dependencies
│
├── .env.example
│   └── Example environment configuration
│
├── .gitignore
│   └── Prevents secrets and local files from being committed
│
└── README.md
    └── Setup and usage instructions
```

---

# 27. Security Reminder

Never commit:

```text
.env
```

Never put:

```text
GROQ_API_KEY=...
```

inside:

```text
simple_rag.py
```

Never commit API keys to GitHub.

If an API key is accidentally committed, revoke/rotate it immediately.

---

# 28. Git Workflow for Learners

After making changes:

```bash
git status
```

Review the files.

Then:

```bash
git add .
```

Commit:

```bash
git commit -m "Add simple RAG application setup"
```

Push:

```bash
git push
```

Before pushing, verify that `.env` is not included:

```bash
git status
```

---

# 29. Expected Final Repository

Your repository should look approximately like:

```text
simple-rag/
│
├── simple_rag.py
├── requirements.txt
├── .env.example
├── .gitignore
└── README.md
```

The following files should NOT be committed:

```text
.env
.venv/
__pycache__/
```

---

# 30. Learning Objectives

After completing this project, you should understand:

- What RAG means
- Why documents are chunked
- What embeddings are
- Why vector databases/vector stores are used
- How FAISS performs similarity search
- How retrieved context is passed to an LLM
- How LangChain connects the components
- How to use Hugging Face embedding models
- How to connect LangChain with Groq
- How to manage API keys using environment variables
- How to create a Python virtual environment
- How to run a Python project from VS Code

---

## Next Steps

Once this basic application is working, the natural progression is:

```text
Level 1
Simple RAG
    ↓
Level 2
RAG using PDF documents
    ↓
Level 3
Multiple documents
    ↓
Level 4
Metadata filtering
    ↓
Level 5
Conversation memory
    ↓
Level 6
RAG evaluation
    ↓
Level 7
RAG with production vector database
    ↓
Level 8
GraphRAG / Neo4j
    ↓
Level 9
Production RAG API
```

The goal is to understand each layer before introducing additional infrastructure.



******************************************************************************************


# Simple RAG Application with Lightweight Evaluation

A beginner-friendly Retrieval-Augmented Generation (RAG) application built with Python, LangChain, Hugging Face embeddings, FAISS and Groq.

This project extends a basic RAG application by introducing a **lightweight custom evaluation framework**.

Instead of only asking:

> "Did the RAG application generate an answer?"

we also ask:

- Did the system retrieve relevant information?
- Is the generated answer correct?
- Is the generated answer supported by the retrieved context?
- How can we automatically test the RAG application?
- Can we run the same evaluation against multiple test questions?

The project is intentionally lightweight so that learners can understand the fundamentals of **RAG evaluation** before moving to dedicated frameworks such as RAGAS, DeepEval, or other evaluation platforms.

---

# 1. What This Application Does

The application contains a small customer banking policy document.

It creates a RAG pipeline that:

1. Creates a document.
2. Splits the document into chunks.
3. Generates embeddings.
4. Stores the embeddings in FAISS.
5. Retrieves relevant chunks for a user question.
6. Sends the retrieved context to a Groq LLM.
7. Generates an answer.

The application then evaluates the RAG pipeline using three evaluation dimensions:

```text
                    RAG APPLICATION
                           │
                           ▼
                    Generated Answer
                           │
              ┌────────────┼────────────┐
              ▼            ▼            ▼
        Answer         Faithfulness   Retrieval
       Correctness                    Quality
```

---

# 2. Why Do We Need RAG Evaluation?

A RAG application can appear to work correctly while still producing poor results.

For example:

```text
User Question
      ↓
Retriever
      ↓
Wrong Document Chunk
      ↓
LLM
      ↓
Plausible but Incorrect Answer
```

The answer may sound convincing even though the retrieved information was incorrect.

Therefore, testing only whether the application runs successfully is not enough.

We need to evaluate different parts of the RAG pipeline.

This project demonstrates that concept with a simple custom evaluation framework.

---

# 3. RAG Pipeline

The application follows:

```text
Source Document
      ↓
Document
      ↓
Chunking
      ↓
Embeddings
      ↓
FAISS Vector Store
      ↓
User Question
      ↓
Similarity Search
      ↓
Retrieved Chunks
      ↓
Context
      ↓
Groq LLM
      ↓
Generated Answer
```

The evaluation layer is then added:

```text
                    ┌──────────────────────┐
                    │      RAG Pipeline    │
                    └──────────┬───────────┘
                               │
                               ▼
                       Generated Answer
                               │
              ┌────────────────┼────────────────┐
              │                │                │
              ▼                ▼                ▼
       Answer Correctness  Faithfulness  Retrieval Quality
              │                │                │
              └────────────────┼────────────────┘
                               ▼
                       Evaluation Summary
```

---

# 4. Technology Stack

| Technology | Purpose |
|---|---|
| Python 3.12.x | Programming language |
| VS Code | Development environment |
| LangChain | RAG components |
| Hugging Face | Embedding model |
| Sentence Transformers | Generates embeddings |
| FAISS | Local vector store |
| Groq | LLM inference |
| python-dotenv | Environment variable management |
| Custom Python functions | Lightweight evaluation framework |

---

# 5. Prerequisites

Before starting, install:

1. Git
2. Python 3.12.x
3. Visual Studio Code
4. VS Code Python extension
5. Groq account
6. Groq API key

You do not need:

- Anaconda
- Docker
- Kubernetes
- A database server
- A GPU
- RAGAS
- DeepEval

The evaluation functionality in this project is implemented directly in Python.

---

# 6. Install Git

## Windows

Download Git:

https://git-scm.com/downloads

Verify:

```bash
git --version
```

---

## macOS

Open Terminal:

```bash
git --version
```

If macOS asks to install Command Line Tools, accept the installation.

---

# 7. Install Python 3.12

This project uses Python 3.12.x.

Python 3.12.5 was used during development/testing of this training material.

Download Python from:

https://www.python.org/downloads/

Python 3.12.5:

https://www.python.org/downloads/release/python-3125/

---

## Windows

During Python installation, make sure you enable:

```text
Add python.exe to PATH
```

Then complete the installation.

Open a new PowerShell window and run:

```powershell
python --version
```

Expected:

```text
Python 3.12.x
```

Verify pip:

```powershell
python -m pip --version
```

If `python` is not recognized:

```powershell
py --version
```

---

## macOS

Verify:

```bash
python3 --version
```

Expected:

```text
Python 3.12.x
```

Verify pip:

```bash
python3 -m pip --version
```

---

# 8. Install Visual Studio Code

Download:

https://code.visualstudio.com/

Install VS Code using the standard installation options.

---

# 9. Install the Python Extension

Open VS Code.

Go to:

```text
Extensions
```

Search for:

```text
Python
```

Install:

```text
Python
Publisher: Microsoft
```

---

# 10. Clone the Repository

Open a terminal.

Navigate to the directory where you want to keep the project.

For example:

```bash
cd Documents
```

Clone the repository:

```bash
git clone <YOUR_GITHUB_REPOSITORY_URL>
```

Example:

```bash
git clone https://github.com/<username>/simple_rag_app_eval.git
```

Move into the project:

```bash
cd simple_rag_app_eval
```

---

# 11. Open the Project in VS Code

Run:

```bash
code .
```

Alternatively:

```text
VS Code
→ File
→ Open Folder
→ simple_rag_app_eval
```

---

# 12. Create a Python Virtual Environment

A virtual environment keeps the dependencies of this project separate from other Python projects.

## Windows

```powershell
python -m venv .venv
```

Activate:

```powershell
.venv\Scripts\Activate.ps1
```

You should see:

```text
(.venv)
```

in the terminal.

If PowerShell blocks activation:

```powershell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```

Then:

```powershell
.venv\Scripts\Activate.ps1
```

---

## macOS

Create:

```bash
python3 -m venv .venv
```

Activate:

```bash
source .venv/bin/activate
```

You should see:

```text
(.venv)
```

---

# 13. Select the Python Interpreter

In VS Code:

```text
Ctrl + Shift + P
```

Windows/Linux

or:

```text
Cmd + Shift + P
```

macOS

Search:

```text
Python: Select Interpreter
```

Select:

```text
.venv
```

For example:

Windows:

```text
.venv\Scripts\python.exe
```

macOS:

```text
.venv/bin/python
```

---

# 14. Upgrade pip

With the virtual environment activated:

```bash
python -m pip install --upgrade pip
```

---

# 15. Install Dependencies

Run:

```bash
pip install -r requirements.txt
```

This installs:

```text
LangChain
Hugging Face
Sentence Transformers
FAISS
Groq integration
python-dotenv
```

---

# 16. Verify Installation

Run:

```bash
pip list
```

You should see packages including:

```text
langchain-core
langchain-community
langchain-text-splitters
langchain-huggingface
langchain-groq
sentence-transformers
faiss-cpu
python-dotenv
```

---

# 17. Create a Groq Account

Go to:

https://console.groq.com/

Sign in or create an account.

---

# 18. Create a Groq API Key

Inside the Groq Console:

1. Open the API Keys section.
2. Create a new API key.
3. Give it a meaningful name.

For example:

```text
simple-rag-app-eval
```

4. Copy the API key.

### Security Warning

Treat the API key like a password.

Never:

- Commit it to Git.
- Put it directly into Python code.
- Push it to GitHub.
- Share it in screenshots.
- Share it in public documentation.

---

# 19. Create the `.env` File

Create this file in the project root:

```text
.env
```

Add:

```text
GROQ_API_KEY=your_actual_groq_api_key
GROQ_MODEL=openai/gpt-oss-120b
```

Example:

```text
GROQ_API_KEY=gsk_xxxxxxxxxxxxx
GROQ_MODEL=openai/gpt-oss-120b
```

Your `.env` file should remain local.

It must NOT be committed to Git.

---

# 20. Why Do We Use `.env`?

The application loads environment variables using:

```python
from dotenv import load_dotenv

load_dotenv()
```

The Groq model configuration is then read from the environment.

This allows us to keep:

```text
API credentials
```

separate from:

```text
Application source code
```

This is an important development and security practice.

---

# 21. Verify `.gitignore`

Make sure `.gitignore` contains:

```text
.env
.venv/
```

Run:

```bash
git status
```

Your `.env` file should not appear as an untracked file.

---

# 22. Run the Application

Run:

```bash
python simple_rag_app_eval.py
```

The application will initialize:

1. Source document
2. Document metadata
3. Text chunks
4. Embedding model
5. FAISS vector store
6. Groq LLM

The first run may take longer because the Hugging Face embedding model needs to be downloaded.

---

# 23. Application Menu

You will see:

```text
======================================================================
RAG + LIGHTWEIGHT EVALUATION
======================================================================

1. Chat with RAG
2. Evaluate RAG
3. Exit

Choose option:
```

The application therefore provides two main modes:

```text
1 → Interactive RAG
2 → Automated RAG Evaluation
3 → Exit
```

The menu and these three execution paths are implemented in the `main()` function.

---

# 24. Option 1 — Chat with RAG

Choose:

```text
1
```

You will enter interactive chat mode.

Example:

```text
Ask question (exit to stop):
```

Try:

```text
How long does the bank take to respond to a complaint?
```

The system:

```text
Question
   ↓
FAISS Retrieval
   ↓
Top 2 Relevant Chunks
   ↓
Context
   ↓
Groq
   ↓
Answer
```

The application also prints the retrieved chunks and their chunk IDs, making it easier to understand what the retriever actually found.

---

# 25. Option 2 — Evaluate RAG

Choose:

```text
2
```

The application executes the predefined evaluation dataset.

The current dataset contains three test cases:

### Test Case 1

```text
Question:
How long does the bank take to respond to a complaint?
```

Expected:

```text
The bank aims to provide a final response to standard complaints within 15 business days.
```

This is an answerable question.

---

### Test Case 2

```text
Question:
What should customers do if their banking credentials are exposed?
```

Expected:

```text
Customers should contact the bank immediately.
```

This is also answerable.

---

### Test Case 3

```text
Question:
What is the savings account interest rate?
```

Expected:

```text
I could not find that information.
```

This is deliberately an unanswerable question.

This is important because a good RAG evaluation dataset should test both:

```text
Questions that CAN be answered
```

and:

```text
Questions that CANNOT be answered
```

Your current dataset explicitly captures that through the `answerable` field.

---

# 26. Evaluation Dimension 1 — Answer Correctness

The first evaluation checks whether the generated answer contains the expected answer.

The implementation:

```python
evaluate_answer(
    actual,
    expected,
    answerable
)
```

first normalizes the generated and expected text.

It then checks:

```text
Expected Answer
       ↓
Is it present in
       ↓
Generated Answer?
```

For an unanswerable question, it checks whether the response contains:

```text
I could not find that information.
```

This is a simple deterministic correctness check.

---

# 27. Evaluation Dimension 2 — Retrieval Quality

The second evaluation asks:

> Did the retriever find a chunk that is sufficiently related to the question?

The process is:

```text
Question
   ↓
Question Embedding
   ↓
Compare with Retrieved Chunk Embeddings
   ↓
Similarity Score
   ↓
Threshold
   ↓
PASS / FAIL
```

The implementation uses the same embedding model used by the RAG application.

A score of:

```text
>= 0.40
```

is currently treated as a pass.

The code explicitly identifies this threshold as a demo-only choice.

---

# 28. Evaluation Dimension 3 — Faithfulness

The third evaluation asks:

> Is the generated answer supported by the retrieved context?

Conceptually:

```text
Retrieved Context
        │
        │
        ▼
Generated Answer
        │
        ▼
Do they contain sufficient overlapping information?
```

The implementation:

1. Normalizes the answer.
2. Normalizes the retrieved context.
3. Extracts words from both.
4. Calculates word overlap.
5. Calculates an overlap ratio.
6. Uses `0.50` as the demonstration threshold.

For an unanswerable question, faithfulness is reported as:

```text
N/A
```

because there is no expected factual answer to validate against.

---

# 29. Important: This Is a Lightweight Evaluation Framework

This project intentionally does NOT use:

```text
RAGAS
DeepEval
LangSmith
TruLens
```

Instead, evaluation is implemented using normal Python functions.

The main evaluation functions are:

```text
evaluate_answer()
evaluate_retrieval()
evaluate_faithfulness()
evaluate_test_case()
run_evaluation()
```

This makes the project useful for learning **why evaluation exists and how an evaluation pipeline can be constructed** before introducing specialized evaluation frameworks.

---

# 30. Complete Evaluation Flow

The evaluation pipeline works like this:

```text
                    Evaluation Dataset
                           │
                           ▼
                     Test Question
                           │
                           ▼
                       RAG Pipeline
                           │
                 ┌─────────┴─────────┐
                 │                   │
                 ▼                   ▼
              Answer             Retrieved Docs
                 │                   │
                 │                   │
        ┌────────┴───────┐     ┌─────┴──────────┐
        │                │     │                │
        ▼                ▼     ▼                ▼
    Correctness      Faithfulness        Retrieval Quality
        │                │                │
        └────────────────┼────────────────┘
                         ▼
                  Test Case Result
                         │
                         ▼
                  Final Summary
```

---

# 31. Final Evaluation Summary

After all test cases are executed, the application calculates:

```text
Answer Correctness : X/3
Faithfulness       : X/3
Retrieval Quality  : X/3
```

The implementation collects the results from every test case and calculates the number of passing cases for each evaluation dimension.

This gives us a very simple RAG quality dashboard:

```text
                RAG QUALITY
                     │
       ┌─────────────┼─────────────┐
       ▼             ▼             ▼
  Correctness    Faithfulness   Retrieval
       │             │             │
       ▼             ▼             ▼
      2/3           2/3           3/3
```

---

# 32. Why This Is Better Than Testing Only the Final Answer

Imagine the application returns:

```text
The bank responds to complaints within 15 business days.
```

It looks correct.

But suppose the retriever actually selected an unrelated chunk.

The LLM may have generated the correct answer because the model already knew the information.

Without retrieval evaluation, we might incorrectly conclude:

```text
RAG is working correctly.
```

Evaluation helps us inspect different stages of the pipeline.

```text
Question
   │
   ├── Retrieval Quality
   │
   ├── Context
   │
   ├── Generated Answer
   │
   ├── Answer Correctness
   │
   └── Faithfulness
```

---

# 33. Important Limitations of This Lightweight Framework

This project is designed for learning.

It should NOT be considered a production-grade evaluation framework.

## Answer Correctness

The current implementation uses text normalization and substring matching.

Therefore:

```text
Expected:
The bank responds within 15 business days.

Generated:
The bank aims to provide a final response within fifteen business days.
```

could potentially be considered incorrect even though the meaning is similar.

A semantic evaluator would handle this more effectively.

---

## Retrieval Quality

The current implementation calculates a dot-product similarity between embeddings.

The threshold:

```text
0.40
```

is explicitly a demonstration threshold rather than a universally valid value.

Different embedding models and datasets can produce different score distributions.

Therefore, production systems should calibrate retrieval thresholds against representative evaluation data.

---

## Faithfulness

The current implementation uses word overlap.

For example:

```text
Context:
Customers should contact the bank immediately if their banking credentials are exposed.

Answer:
If your banking credentials are compromised, contact the bank immediately.
```

These statements have similar meaning, but simple word overlap may underestimate their semantic similarity.

A production evaluation system would generally use more sophisticated semantic or model-based evaluation.

---

# 34. Lightweight Framework vs Dedicated Evaluation Frameworks

This project demonstrates the fundamentals.

A simplified conceptual comparison:

| Capability | This Project | RAGAS | DeepEval |
|---|---|---|---|
| Easy to understand | Yes | Moderate | Moderate |
| Custom Python evaluation | Yes | Yes | Yes |
| Answer correctness | Basic | Advanced metrics available | Advanced metrics available |
| Retrieval evaluation | Basic | Yes | Yes |
| Faithfulness | Basic | Yes | Yes |
| Semantic evaluation | Limited | Yes | Yes |
| LLM-as-a-judge | No | Supported | Supported |
| Production-ready evaluation platform | No | More advanced | More advanced |
| Best for learning fundamentals | Yes | After fundamentals | After fundamentals |

The important lesson is:

> You don't need a sophisticated evaluation framework to understand the principles of RAG evaluation.

Start with deterministic tests and understand what you are measuring.

Then introduce specialized frameworks when the application becomes more complex.

---

# 35. Suggested Learning Progression

```text
Level 1
Basic RAG
    │
    ▼
Level 2
Add Evaluation Dataset
    │
    ▼
Level 3
Answer Correctness
    │
    ▼
Level 4
Retrieval Evaluation
    │
    ▼
Level 5
Faithfulness Evaluation
    │
    ▼
Level 6
Dedicated Framework
(RAGAS / DeepEval)
    │
    ▼
Level 7
LLM-as-a-Judge
    │
    ▼
Level 8
Continuous RAG Evaluation
    │
    ▼
Level 9
Production Observability
```

---

# 36. Project Structure

```text
simple_rag_app_eval/
│
├── simple_rag_app_eval.py
│   └── Complete RAG + evaluation application
│
├── requirements.txt
│   └── Python dependencies
│
├── .env.example
│   └── Example environment configuration
│
├── .gitignore
│   └── Prevents secrets and local files from being committed
│
└── README.md
    └── Setup, usage and evaluation documentation
```

---

# 37. Important Functions

The main functions in the application are:

```text
rag_pipeline()
```

Runs the RAG pipeline.

```text
evaluate_answer()
```

Evaluates answer correctness.

```text
evaluate_retrieval()
```

Evaluates retrieval relevance.

```text
evaluate_faithfulness()
```

Evaluates whether the answer is supported by retrieved context.

```text
evaluate_test_case()
```

Runs all evaluations for one test case.

```text
run_evaluation()
```

Runs the complete evaluation dataset.

```text
chat_mode()
```

Provides interactive RAG chat.

```text
main()
```

Provides the application menu.

---

# 38. Adding New Evaluation Test Cases

You can add additional test cases to:

```python
evaluation_dataset
```

Example:

```python
{
    "question": "Can a suspicious transaction be temporarily held?",
    "expected_answer": "The bank may temporarily hold a suspicious transaction while verification is completed.",
    "answerable": True
}
```

You can also add an unanswerable question:

```python
{
    "question": "What is the mortgage interest rate?",
    "expected_answer": "I could not find that information.",
    "answerable": False
}
```

This allows you to gradually build a larger evaluation dataset.

---

# 39. Recommended Evaluation Dataset

As the application grows, include different categories:

```text
1. Direct factual questions
2. Paraphrased questions
3. Multi-part questions
4. Questions requiring multiple chunks
5. Unanswerable questions
6. Ambiguous questions
7. Out-of-domain questions
8. Adversarial questions
```

This gives you better coverage than testing only a few obvious questions.

---

# 40. Common Problems and Solutions

## Problem 1 — Python not found

Windows:

```powershell
python --version
```

or:

```powershell
py --version
```

macOS:

```bash
python3 --version
```

---

## Problem 2 — pip not found

Use:

```bash
python -m pip install -r requirements.txt
```

On macOS:

```bash
python3 -m pip install -r requirements.txt
```

---

## Problem 3 — Wrong Python interpreter

In VS Code:

```text
Command Palette
→ Python: Select Interpreter
→ Select .venv
```

---

## Problem 4 — Groq API error

Check that `.env` exists:

```text
simple_rag_app_eval/
├── simple_rag_app_eval.py
├── requirements.txt
├── .env
└── README.md
```

And contains:

```text
GROQ_API_KEY=your_actual_key
```

---

## Problem 5 — Groq model error

Groq periodically changes its available models.

Check the current model list:

https://console.groq.com/docs/models

Then update:

```text
GROQ_MODEL=...
```

inside `.env`.

---

## Problem 6 — FAISS installation problem

Upgrade pip:

```bash
python -m pip install --upgrade pip
```

Then try:

```bash
pip install faiss-cpu
```

---

## Problem 7 — Hugging Face model download

The first execution downloads:

```text
sentence-transformers/all-MiniLM-L6-v2
```

This may take some time.

A network connection is required for the initial model download.

---

# 41. Git Workflow

Check the repository:

```bash
git status
```

Add files:

```bash
git add .
```

Commit:

```bash
git commit -m "Add RAG application with lightweight evaluation"
```

Push:

```bash
git push
```

Before pushing, verify that:

```text
.env
.venv/
```

are not included.

---

# 42. Expected Repository

Your Git repository should contain:

```text
simple_rag_app_eval/
│
├── simple_rag_app_eval.py
├── requirements.txt
├── .env.example
├── .gitignore
└── README.md
```

Do NOT commit:

```text
.env
.venv/
__pycache__/
```

---

# 43. Learning Objectives

After completing this project, you should understand:

### RAG

- Document creation
- Chunking
- Embeddings
- Vector stores
- Similarity search
- Context retrieval
- Prompt construction
- LLM generation

### RAG Evaluation

- Why RAG evaluation is required
- Evaluation datasets
- Answer correctness
- Retrieval quality
- Faithfulness
- Answerable vs unanswerable questions
- Evaluation thresholds
- PASS / FAIL evaluation
- Aggregating test results

### Engineering

- Python virtual environments
- Dependency management
- Environment variables
- API key management
- VS Code setup
- Git workflow

---

# 44. Final Takeaway

A RAG application should not be evaluated only by asking:

```text
"Does it produce an answer?"
```

Instead, we should ask:

```text
Did we retrieve the right information?

Did the generated answer correctly answer the question?

Is the answer supported by the retrieved context?

Does the system behave correctly when the answer is not available?
```

This project provides a simple way to introduce those concepts before moving to dedicated RAG evaluation frameworks.

The next step is to replace or enhance these lightweight checks with more sophisticated evaluation approaches such as semantic similarity, LLM-as-a-judge, RAGAS, DeepEval, and production observability.