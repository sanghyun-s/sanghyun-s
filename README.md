# Hi, I'm Sang-Hyun Seong 👋

I work at the intersection of accounting, analytics, and business systems.

I'm an M.S. in Business Analytics candidate at Baruch College (CUNY, Zicklin — expected May 2027) with prior U.S. small-business accounting experience. I'm building toward analytics and business-systems roles, using accounting as my strongest domain context, with applied AI and workflow development as a differentiator.

---

## Background

Before graduate school I spent a year as a staff accountant at a Los Angeles accounting firm, working with 30+ small-business clients. I carried end-to-end bookkeeping responsibilities — reconciliations, GL maintenance, AP/AR, payroll-related workflows, adjusting and year-end entries, and financial-statement support — and worked on tax returns as a supporting preparer under senior and CPA review, coordinating with clients and government agencies along the way.

I earned a B.S. in Business Administration from Boston University (Questrom — Information Systems & Strategy and Innovation) before moving into accounting.

That experience defined the problem space for the portfolio below. PREPARE is its most direct descendant; CASSIA and LUCENT developed through later research into accounting, data, systems, and workflow problems.

---

## Accounting Meets AI — Gen 1

Over roughly half a year I researched, refined, built, tested, and deployed three applications, each around a specific accounting workflow. I use AI-assisted development extensively, while owning the problem definition, domain interpretation, workflow design, scope, testing, validation, and product decisions behind each one.

**[PREPARE](https://github.com/sanghyun-s/PREPARE) — Reconciliation Prep Engine** · v2.0 · [live](https://prepare-recon.onrender.com/)

Turns bank and credit card statement PDFs into classified, reconciled, review-ready Excel workpapers for 1099 pre-review — deliberately not a filer. The design principle is *Transcribe, Don't Compute*: the model reads and labels each row, while deterministic server logic does the arithmetic, so a statement whose stated math doesn't balance gets flagged instead of silently corrected. Two independent integrity checks separate statement arithmetic problems from extraction gaps, so the reviewer knows what to do next.
*Python · FastAPI · Claude Agent SDK · openpyxl · JavaScript*

**[CASSIA](https://github.com/sanghyun-s/cassia) — Chat-based Accounting System for Search, Insight & Analysis** · v2.12 · [live](https://cassia-utwt.onrender.com/)

A support workspace that answers plain-English accounting questions across structured and unstructured sources. A router sends each question to Text-to-SQL over the books, retrieval over IRS publications and uploaded documents, or both, and returns a grounded answer with tables, citations, and charts. Findings can be saved and recalled later by meaning rather than exact wording.
*Python · FastAPI · SQL · RAG · ChromaDB · OpenAI API · Plotly*

**[LUCENT](https://github.com/sanghyun-s/lucent-pre-audit-review-packet) — Pre-Audit Review Packet** · [live](https://lucent-frontend.onrender.com/)

Takes a QuickBooks-style general-ledger export and narrows it to a prioritized review queue. Anomaly detection surfaces statistically unusual entries, materiality thresholds and qualitative overrides apply accounting judgment, and a validated memo layer explains what to check and what evidence to request. The framing is *risk indication, not fraud detection* — the tool prioritizes, the human concludes.
*Python · FastAPI · scikit-learn · Next.js · OpenAI API*

---

## Analytics & Technical Development

**Analytics.** Python, SQL, Excel, Tableau, and relational database design through graduate coursework and applied projects.

**Applied systems.** FastAPI, RAG and Text-to-SQL, scikit-learn, API integration, Git/GitHub, and Render deployment through the Gen 1 portfolio.

**Current development.** I'm deepening Power BI, R, independent SQL and Python fluency, and cloud and data-systems tools including AWS, Docker, and OpenSearch — supported by Fall 2026 coursework in Big Data Technologies (CIS 9760), Basic Software Tools (STA 9750, R), and Business Analytics Project Management (BUS 9430).

---

## Technical Reinforcement

Alongside the portfolio, I maintain a public **[Technical Reinforcement Log](https://github.com/sanghyun-s/technical-reinforcement-log)** to make the underlying SQL, Python, BI, R, and cloud skills independently reproducible and interview-defensible — through coursework, coding drills, artifacts, and cold practice. The standard is what I can reproduce, explain, and defend on my own.

---

## What I'm Building Toward

With the three Gen 1 applications deployed, I'm continuing to harden and refine their technical foundations. My longer-term direction is interoperability across accounting workflows: how data moves between bookkeeping, payroll, tax, and review with deterministic validation, clear system boundaries, safer data handling, and tests that hold. **FS Cross-Check** — a financial-statement tie-out and mapping tool — is the first major build I plan to use to explore this direction.

---

## Connect

- **LinkedIn:** [sam-seong](https://www.linkedin.com/in/sam-seong/)
- **GitHub:** [sanghyun-s](https://github.com/sanghyun-s)
- **Live apps:** [PREPARE](https://prepare-recon.onrender.com/) · [CASSIA](https://cassia-utwt.onrender.com/) · [LUCENT](https://lucent-frontend.onrender.com/) — free-tier hosting; allow up to a minute for an idle app to wake.
