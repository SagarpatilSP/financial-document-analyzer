# 📊 Financial Document Analyzer (CrewAI Debug Challenge)

## 🚀 Overview

This project is a fixed and enhanced version of the provided CrewAI-based Financial Document Analyzer system.

The original repository contained:
- Deterministic runtime bugs
- Improper CrewAI tool usage
- Hallucination-prone prompts
- Unsafe financial advice generation
- Poor architecture design

This version:
- Fixes all deterministic bugs
- Refactors tools to proper CrewAI format
- Rewrites prompts for structured, evidence-based analysis
- Improves architecture
- Adds optional scalability enhancements

---

# 🐛 Bugs Found & Fixes

## 1️⃣ Undefined LLM Initialization
**Issue:**  
`llm = llm` caused immediate runtime failure.

**Fix:**  
Proper LLM initialization using CrewAI LLM class.

---

## 2️⃣ Missing PDF Loader Import
**Issue:**  
`Pdf` class was used but never imported.

**Fix:**  
Replaced with:
```python
from langchain_community.document_loaders import PyPDFLoader

---

3️⃣ Improper Tool Structure

Issue:
FinancialDocumentTool was a static function and not a proper CrewAI Tool.

Fix:
Refactored to inherit from BaseTool with _run() method.

---

4️⃣ Async Misuse

Issue:
Async methods were defined but not awaited.

Fix:
Converted to synchronous _run() implementation.

---

5️⃣ File Not Passed to Crew

Issue:
Uploaded file path was never passed to agents.
	financial_crew.kickoff({
    	"query": query,
    	"file_path": file_path
	})

---

⚙️ Setup Instructions
1️⃣ Clone Repository
git clone <your-repo-link>
cd financial-document-analyzer

2️⃣ Create Virtual Environment
python -m venv venv
source venv/bin/activate      # Mac/Linux
venv\Scripts\activate         # Windows

3️⃣ Install Dependencies
pip install -r requirements.txt

4️⃣ Create .env File

Create a .env file in the root directory:

OPENAI_API_KEY=your_api_key_here

5️⃣ Run the Application
uvicorn main:app --reload


📘 API Documentation
🔹 GET /

Health check endpoint.

Response
{
  "message": "Financial Document Analyzer API is running"
}
🔹 POST /analyze
Request

Form Data:

file: PDF file (required)

query: Optional string

Example (cURL)
curl -X POST "http://localhost:8000/analyze" \
  -F "file=@financial_report.pdf" \
  -F "query=Analyze financial health and provide investment recommendation"
Response Format
{
  "status": "success",
  "query": "Analyze financial health...",
  "analysis": "Structured financial analysis output",
  "file_processed": "financial_report.pdf"
}
