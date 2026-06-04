# Hi, I'm Sang-Hyun Seong 👋

Accounting professional building AI-powered tools for the profession I know best.

Currently pursuing my **Master's in Business Analytics at Baruch College, CUNY**, with a Bachelor's in Business Administration from **Boston University**. Also training through the **Gen AI × Accounting** curriculum (Global AI Bootcamp), combining real accounting experience with full-stack development to build practical tools — not demos.

---

## 🔧 What I'm Building: Accounting Meets AI

A portfolio of connected AI-powered accounting workflow tools, each tackling a specific pain point I encountered as a junior accountant. Each app is designed to stand alone while interoperating with the others through a shared foundation.

### Shipped — May 2026

**[PREPARE](https://github.com/sanghyun-s/PREPARE) — Reconciliation Prep Engine** *(v2.0)*

Turns messy bank and credit card statement PDFs into review-ready 1099 pre-reconciliation workbooks. Not a 1099 filer — the deliverable is the workbook a CPA reviews *before* filing.

Key capabilities:
- Row-level transaction classification via Claude PDF Skill (Agent SDK) — distinguishes vendor payments from payroll deposits, balance lines, transfers, and bank fees that a naive parser would lump together
- Per-statement reconciliation snapshot — verifies the statement's stated math balances, built on a *Transcribe, Don't Compute* principle so the AI never silently smooths discrepancies
- Extraction completeness cross-check — orthogonal to the reconciliation snapshot, catches missed rows independently
- Five-sheet master Excel workbook plus per-statement workbooks with full audit trail

*Stack:* Python · FastAPI · Claude Agent SDK (Sonnet/Opus) · openpyxl · vanilla JS

### In development

**[CASSIA — Chat-based Accounting System](https://github.com/sanghyun-s/accounting-ai-chatbot)** — Hybrid RAG + Text-to-SQL chatbot for QuickBooks data. Ask questions about your books in plain English; the router classifies the query, runs the right pipeline (SQL execution or IRS regulation retrieval), and returns the answer with an auto-generated chart.

**[AI Audit Risk Analyzer](https://github.com/sanghyun-s/ai-audit-risk-analyzer)** — ML anomaly detection (Isolation Forest) plus GPT narrative synthesis to surface and explain audit risks in GL transaction data. Flags round-number patterns, year-end clustering, and vendor anomalies, then generates PCAOB-aligned risk summaries.

### Coming next

Two more apps planned for late 2026 — focused on IRS form extraction and tax-schedule classification. Each reuses production code from the shipped apps, scoped tightly to one domain-specific question rather than trying to do everything at once.

### Shared foundation

**[Transaction Agent Ultimate (TAU)](https://github.com/sanghyun-s/transaction-agent-ultimate)** — Originally the experimental prototype where these apps started. Now evolving into a **demonstration hub** where viewers can try minor versions of each shipped app as sidebar add-ons, with one canonical place to see how the portfolio fits together.

---

## 🎯 Engineering Principles I'm Learning From These Projects

Building real accounting tools (rather than generic demos) has surfaced a few design principles that keep recurring across the portfolio:

- **Transcribe, Don't Compute.** AI is allowed to read and label; deterministic logic does the arithmetic. Protects against AI silently "fixing" discrepancies by adjusting numbers until they balance.

- **Arithmetic in one place.** Computation lives in the pipeline; the frontend and Excel outputs display the same numbers, never recompute. Duplicate computation paths invite drift between surfaces.

- **Scope discipline.** When a feature drifts toward decisions the app doesn't have evidence for (e.g., 1099 filing decisions in PREPARE), the right move is to draw a boundary and split it into a separate app. Honest scope makes the tool more trustworthy.

- **Diagnostic-before-edit.** Before changing any live file, verify state with grep. Patch-by-patch with verification between each. Slower than batched edits; robust against the kind of bug that breaks production in non-obvious ways.

---

## 💼 Background

- **Accounting experience** at Rowshan & Co (Korean-American tax firm) — 1099/W-2 processing, QuickBooks bookkeeping, client engagements
- **CPT training** in QuickBooks and general ledger management
- **Education:** M.S. Business Analytics, Baruch College (CUNY) · B.S. Business Administration, Boston University
- **Currently:** building this portfolio through the Global AI Bootcamp's Gen AI × Accounting curriculum, alongside graduate coursework

Every app in the portfolio originates from a specific frustration I had on the job. PREPARE comes from manual 1099 reconciliation that took hours every tax season. CoReckoner comes from clients asking the same Q&A questions every quarter. AI Audit Risk Analyzer comes from the manual GL review work that auditors spend days on. The goal isn't "AI for accounting" in the abstract — it's specific tools for specific tasks I lived through.

---

## 🛠️ Tech Stack

**Languages:** Python, JavaScript

**Backend:** FastAPI, Pydantic, uvicorn

**Frontend:** Next.js, React, vanilla JS, CSS

**AI/ML:** 
- Anthropic Claude (Agent SDK, PDF Skill, Sonnet/Opus models)
- OpenAI API (GPT-4o-mini)
- LangChain, ChromaDB
- scikit-learn (Isolation Forest, classification)
- Prompt engineering (few-shot, chain-of-thought, structured output via JSON schema)

**Data:** pandas, openpyxl, pdfplumber, SQLite

**Tools:** Git, GitHub, VS Code, Claude Code, npm, pip, virtualenv

---

## 🌱 What I'm Working On Improving

I'm still early in my software engineering journey, and the projects above have surfaced specific gaps I'm working on:

- **System design under iteration.** PREPARE went through five major architectural phases. Learning to anticipate which decisions will hold up versus which will need to be redone is the slow skill.
- **Testing discipline.** Most of my testing is currently manual and visual. Building proper unit and integration test coverage is the next phase.
- **Deployment.** The apps run locally; production deployment (Docker, hosting, CI/CD) is on the immediate roadmap.
- **Cross-app data flow.** As the portfolio grows, how apps share data and state cleanly is a real architectural question I'm still working through.

---

## 📫 Connect

- **GitHub:** [sanghyun-s](https://github.com/sanghyun-s)
- **Education:** M.S. Business Analytics, Baruch College (CUNY) · B.S. Business Administration, Boston University
- **LinkedIn:** *[(https://www.linkedin.com/in/sam-seong/)]*

*Currently writing about the PREPARE v2.0 development arc on LinkedIn — design decisions, scope cuts, and engineering principles that emerged during the build.*
