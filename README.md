# Hi, I'm Sang-Hyun Seong 👋

Accounting professional building AI-powered tools for the profession I know best.

I'm pursuing my **M.S. in Business Analytics at Baruch College (CUNY)** — Zicklin School of Business, Data Analytics concentration, expected May 2027 — after a **B.S. in Business Administration from Boston University** (Questrom, Information Systems & Strategy and Innovation). Alongside graduate coursework I'm training through the **Gen AI × Accounting** curriculum (Global AI Bootcamp), combining real accounting experience with full-stack development to build practical tools.

Before graduate school I spent a year as a **staff accountant at a public accountancy firm**, doing full-cycle bookkeeping and tax-season work for 30+ small-business clients. Every app below traces back to a specific frustration I lived through on that job.

---

## 🔧 Accounting Meets AI

A portfolio of connected AI-powered accounting workflow tools, each tackling a specific pain point I encountered as a junior accountant. Each app stands alone while interoperating with the others through a shared foundation.

The portfolio is scoped as a **finite project with a defined endpoint**. It reaches completion when five domain apps ship — three main apps (**PREPARE**, **CASSIA**, **LUCENT**) and two I'm designing and building on my own (**IRS Form Processor**, **Tax Schedule Classifier**) — and every one of them is then distilled back into **TAU**, a single hub where each runs as a compact add-on. TAU is where the portfolio started as a prototype, and it's where the whole thing is meant to converge. That loop — prototype → five standalone apps → back into one hub — is the finish line.

The goal was never "AI for accounting" in the abstract. It's specific tools for specific tasks I actually did by hand.

---

### 🚀 Deployed

**[PREPARE](https://github.com/sanghyun-s/PREPARE) — Reconciliation Prep Engine** *(v2.0 · deployed)*

Turns messy bank and credit card statement PDFs into review-ready 1099 pre-reconciliation workbooks. Deliberately **not a 1099 filer** — the deliverable is the workbook a CPA reviews *before* filing.

The core insight is that this isn't a parsing problem, it's an accounting-classification problem. A $1,500 row might be a vendor payment (1099-relevant), a payroll deposit (excluded), a balance line (not a transaction), a transfer, or a bank fee. PREPARE extracts every row and says *what kind* of row each one is.

- **Row-level classification** via Claude PDF Skill (Agent SDK, Sonnet default / Opus optional) — distinguishes vendor payments from payroll deposits, balance lines, transfers, and fees a naive parser would lump together.
- **Two orthogonal integrity checks.** *Source A* asks "does the statement's stated math balance?"; *Source B* asks "did we extract every row the statement reported?" Because they can fail independently, together they place each statement in one of four diagnostic states — telling the reviewer *what to do next* rather than collapsing everything into one ambiguous warning.
- **Transcribe, Don't Compute.** The AI reads and labels; deterministic logic does the arithmetic — so the model can never silently "fix" a discrepancy by nudging numbers until they balance. In live testing it surfaced a $150 arithmetic gap and flagged the statement instead of papering over it.
- **Three surfaces, three questions.** Per-Statement (is this statement trustworthy as a unit?), Consolidated Validation (across statements, what needs review?), and Excel workbooks (the full audit-ready evidence).

*Measured on the reference test set:* 100% row-classification accuracy, 1–4 min and $0.12–$0.60 per PDF (Sonnet).

*Stack:* Python · FastAPI · Claude Agent SDK · openpyxl · vanilla JS

<br>

**[CASSIA](https://github.com/sanghyun-s/cassia) — Chat-based Accounting System** *(v2.12.1 · deployed · no-login)*

*Previously built under the working name CoReckoner.* A chat-based accounting **support** workspace for small-business follow-up work — client questions, agency notices, and the follow-up tasks that sit on the support side of a practice, distinct from the bookkeeping/reconciliation/calculation tools. The workflow mirrors how accountants already work: **Ask → Retrieve → Visualize → Save → Organize → Recall → Follow up → Export.**

- **Hybrid router.** Ask in plain English; the router classifies the query and runs the right pipeline — **Text-to-SQL** over the books, **RAG** over IRS publications, **BOTH** merged, or **Core recall** of your saved work — returning a grounded answer with citations, a table, and an auto-generated chart.
- **Semantic recall.** Save any answer or upload to a permanent "core," then pull it back months later by meaning ("what did I save about Q1 net income?"), not by exact title.
- **Per-session document Q&A** with per-user vector isolation, multilingual answers (incl. Korean), export to Markdown / print-HTML / CSV, and heuristic SSN/EIN masking.

**Deployment note:** Deployed on Render on **2026-06-28**; **login removed 2026-07-01** in favor of a no-login, anonymous per-browser workspace — a deliberate go-to-market call, since a name/email gate in front of a free tool suppresses first use. The full Phase-5 account system (bcrypt, server-side sessions, per-user isolation) is **retained in the codebase but frozen**, and can be re-enabled without a rewrite. Phases 1–6 complete, verified end-to-end across four accounting business-case simulations.

*Stack:* FastAPI (Python 3.13) · OpenAI gpt-4o-mini + text-embedding-3-small · ChromaDB · SQLite · LangChain · vanilla JS + Plotly

<br>

### 🛠️ Build complete · deployment next

**[LUCENT](https://github.com/sanghyun-s/lucent-pre-audit-review-packet) — Pre-Audit Review Packet** *(Phases 1–5 shipped · deployment next)*

*Ledger Understanding, Control Evidence & Narrative Triage* — rebranded from ARGUS. Upload a company-level QuickBooks-style general ledger, and LUCENT narrows a large transaction population into a prioritized review queue, explains each risk indicator in plain language, and shows what evidence to request — before a close, CPA handoff, audit readiness, or investor diligence.

The framing is deliberate: **risk indication, not fraud detection.** A real client GL never arrives with confirmed fraud labels, so a fraud detector can't be honest — LUCENT indicates risk and the human concludes. Three layers, three jobs:

1. **ML finds** — Isolation Forest (200 trees, label-free) surfaces rows that stand out statistically.
2. **Audit logic adjusts** — a materiality filter (the only step that can *lower* a tier) plus a PCAOB **AS 2401 qualitative override** (2+ co-occurring red flags escalate a row *above* its raw ML tier, because pattern beats dollar size).
3. **GPT explains** — a validated 7-field review memo (risk summary, assertion, magnitude, likelihood, control/COSO, evidence-to-request, verbatim disclaimer), guarded by a strict validator (schema, length, banned-phrase scan, name-leakage) with a deterministic fallback that's valid by construction. GPT translates; it never decides.

Everything is anchored to real standards (AU-C 315, PCAOB AS 2401 / AS 2201, COSO 2013) as design rationale — never as a claim of performing an audit.

*Next up (Phase 6):* deployment (Vercel + Render/Fly.io), repo rename, a rule-based Standards Grounding panel, Excel export, and CI/CD.

*Stack:* FastAPI (Python 3.13) · Next.js 14 · React 18 · scikit-learn · OpenAI gpt-4o-mini · Tailwind · shadcn/ui · Plotly

<br>

### 🧭 Designing & building next (self-directed)

**IRS Form Processor — Guided 1099 / W-9 Preparation Workspace**

A tax-information-return preparation and review workspace for small-firm accounting teams, following a **Collect → Extract → Match → Validate → Review → Export** flow. It collects vendor identity data and payment records, detects 1099 payment candidates from the books, extracts form fields, validates TIN / missing-field / books-vs-form issues, prepares a 1096 summary worksheet, and exports review-ready workpapers for accountant approval. Preparation and review only — **not** an e-file or filing system. Born directly from the manual 1099/W-2 tax-season work I did at the firm, and from the observation (surfaced during PREPARE) that TIN/EIN identity, not name normalization, is the real filing-level problem.

**Tax Schedule Classifier — Vendor-to-Tax Schedule Mapping Assistant**

Reviews vendor payments, GL, and P&L detail and **proposes likely Schedule C / E / F line-item candidates** with reasoning, confidence scores, and review flags for tax-preparer approval. The emphasis is on *proposing candidates*, not "matching" — the same vendor lands on different schedules depending on activity context (a repair at a sole-prop office → Schedule C; at a rental unit → Schedule E; on farm equipment → Schedule F). MVP starts with a Schedule C expense classifier. An independent app that can *later* accept PREPARE or IRS Form Processor outputs as supporting inputs. It does not prepare or file a return — it prepares schedule-classification workpapers for human review.

<br>

### 🧩 The hub — where it converges

**[TAU](https://github.com/sanghyun-s/transaction-agent-ultimate) — Transaction Agent Ultimate**

Originally the experimental prototype where this whole portfolio started, TAU is evolving into the **demonstration hub** — the one canonical place to see how the pieces fit. As each standalone app matures, its core is compressed into a compact TAU add-on (a Statement Reconciliation Review page, a Consolidated Workbook Builder, a Data & Document Chat), so viewers can try a minor version of every app in one place. Standalone apps are full workflow *products*; TAU add-ons are compact workflow *tools*. When all five apps have been minimized back into TAU, the mother project is done.

---

## 🎯 Engineering principles I'm learning from these projects

Building real accounting tools (rather than generic demos) surfaced a few principles that keep recurring across the portfolio:

- **Transcribe, Don't Compute.** AI reads and labels; deterministic logic does the arithmetic. Protects against the model silently "fixing" discrepancies by adjusting numbers until they balance.
- **Arithmetic in one place.** Computation lives in the pipeline; the frontend and Excel outputs display the same numbers, never recompute. Duplicate computation paths invite drift between surfaces.
- **Scope discipline.** When a feature drifts toward decisions the app has no evidence for (1099 filing calls in PREPARE; fraud conclusions in LUCENT), the honest move is to draw a boundary and split it into a separate app. Honest scope makes a tool more trustworthy.
- **Validate, then fall back.** LLM output passes a strict validator (schema, length, banned-phrase, name-leakage) before display, with a deterministic fallback that's correct by construction — so the app stays usable and safe even when the model or the API isn't.
- **Diagnostic-before-edit.** Before touching any live file, verify state with grep. Patch-by-patch with verification between each. Slower than batched edits; robust against the bugs that break production in non-obvious ways.
- **Phased delivery with dev notes.** Every meaningful capability ships as a numbered phase with a written dev note — what shipped, what was rejected, what broke, and how to resume. It's what makes the work durable across long gaps.

---

## 💼 Background

**Staff Accountant (Bookkeeping & Tax Return Assistant)** · Rowshan & Co Accountancy Firm — *Jun 2024 – Jun 2025*

- Managed full-cycle bookkeeping for **30+ small-business clients** in QuickBooks Online and Desktop — bank and credit card reconciliations, general ledger maintenance, adjusting journal entries.
- Prepared monthly financial statements and supported payroll, sales tax, business-license, and year-end compliance across multiple client entities.
- Investigated account discrepancies against prior-period records and source documents, producing organized, audit-ready workpapers for CPA review.
- Coordinated directly with clients and government agencies (IRS, EDD, FTB) to obtain documentation and resolve payroll and tax issues.

This is the origin of the portfolio: PREPARE comes from the manual 1099 reconciliation that ate hours every tax season; CASSIA from clients asking the same follow-up questions every quarter; LUCENT from the manual GL review that takes auditors days; the IRS Form Processor from re-keying 1099/W-9 data by hand.

**Education**

- **M.S. Business Analytics**, Baruch College (CUNY), Zicklin School of Business — *expected May 2027* · Data Analytics concentration · CPA 150-credit education requirement eligible · GPA 3.7 · coursework in Programming in Analytics, Database Management, Applied NLP, Accounting Analytics.
- **B.S. Business Administration**, Boston University, Questrom School of Business — *May 2024* · Information Systems & Strategy and Innovation.

**Leadership**

- **Vice President, Digital Marketing** — Zicklin Graduate Tax Society *(Sep 2025 – Present)*
- **Volunteer Korean Language Instructor** — Global Language Network *(Sep 2024 – Dec 2024)*

---

## 🛠️ Tech stack & skills

**Languages:** Python · JavaScript · SQL

**Accounting & Finance:** QuickBooks Online/Desktop · full-cycle bookkeeping · GL maintenance · bank & credit card reconciliation · payroll processing · payroll & sales-tax compliance · financial-statement preparation · 1099 pre-review

**AI / ML:** Anthropic Claude (Agent SDK, PDF Skill, Sonnet/Opus) · OpenAI API (gpt-4o-mini, text-embedding-3-small) · Retrieval-Augmented Generation (RAG) · Text-to-SQL · LangChain · ChromaDB · scikit-learn (Isolation Forest, Random Forest) · anomaly detection · prompt engineering (few-shot, chain-of-thought, structured JSON output)

**Application development:** FastAPI · Pydantic · uvicorn · Next.js 14 · React 18 · shadcn/ui · Tailwind · REST APIs · vanilla JS · HTML/CSS · Plotly

**Data & BI:** pandas · openpyxl · pdfplumber · SQLite · data cleaning & validation · statistical analysis · Excel automation · Power BI · Tableau

**Business systems:** Microsoft Excel (PivotTables, Power Query, XLOOKUP, INDEX-MATCH, SUMIFS) · ADP · AMS Payroll

**Tools:** Git · GitHub · VS Code · Claude Code · npm · pip · virtualenv

**Languages (spoken):** Korean (native) · English (fluent)

---

## 🌱 What I'm working on improving

I'm still early in my software-engineering journey, and these projects have surfaced specific gaps I'm working on:

- **System design under iteration.** PREPARE went through five major architectural phases. Learning to anticipate which decisions will hold versus which need redoing is the slow skill.
- **Testing discipline.** Much of my testing is still manual and visual; building proper unit and integration coverage is the next phase (LUCENT's ~145-assertion contract suite is a step in that direction).
- **Deployment & ops.** CASSIA is live on Render and LUCENT deploys next, but containerization, hosting, and CI/CD across the whole suite are still on the roadmap.
- **Cross-app data flow.** As the portfolio converges into TAU, how apps share data and state cleanly is a real architectural question I'm working through.

---

## 📫 Connect

- **GitHub:** [sanghyun-s](https://github.com/sanghyun-s)
- **LinkedIn:** [sam-seong](https://www.linkedin.com/in/sam-seong/)
- **Education:** M.S. Business Analytics, Baruch College (CUNY) · B.S. Business Administration, Boston University

*Currently writing on LinkedIn about the build arc of these apps — the design decisions, the scope cuts, and the engineering principles that emerged along the way.*
