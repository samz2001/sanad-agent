# Sanad (سند)

A RAG-based agent that answers questions about Saudi employment contract regulations.

Sanad reads an employment contract, checks it against the official regulatory framework published by the Ministry of Human Resources and Social Development (MHRSD), and answers with a reference to the exact article it relied on.

Built as a capstone project for the SDA Agentic AI Bootcamp (Group 07) by Sarah Alzahrani, Dalal Alqahtani, and Hessa Alnajashi.

## What it does

Sanad does more than question answering. For a contract it will:

1. **Analyse** the query and the attached contract against the retrieved statutory articles.
2. **Rate** the contract against official regulations and flag missing required terms.
3. **Answer** with a clear explanation backed by the article reference and version date.

## Features

- Analyse and rate an employment contract
- Compare two contracts side by side
- Salary benchmarking across saved contracts
- Optional saved contracts: users are asked before anything is stored, and nothing is kept without consent
- Bilingual: Arabic and English

## Who it is for

**Employees** asking what they are owed: wages and payment terms, annual and sick leave, probation conditions, notice periods, end of service award.

**Employers, companies, and HR teams** asking whether a contract is safe to issue: required clauses, remote and part-time arrangements, flexible work compliance, rules for non-Saudi employees.

## Sources

All retrieval is grounded in seven official MHRSD documents:

- Labor Law → نظام العمل
- Implementing Regulation → اللائحة التنفيذية
- Unified Contract Template → نموذج العقد الموحد
- Flexible Work Regulation → تنظيم العمل المرن
- Wage Protection System → حماية الأجور
- Ministerial decisions on remote and part-time work → قرارات وزارية
- Provisions for non-Saudi employees → أحكام غير السعوديين

## Architecture

**Ingestion**

Official PDFs from MHRSD → parsed into parts, chapters, and articles → metadata attached (source, article number, version) → embedded and stored in a vector database.

**Query**

Question in Arabic or English → retrieval over article chunks → analyse, rate, then answer → answer returned with its article reference.

## Tech stack

This stack is subject to change as the project develops.

- Frontend → React
- Backend → Python / FastAPI
- LLM → GPT-4o-mini
- Evaluation → RAGAS

Evaluation covers correctness, faithfulness, relevance, and context retrieval. Answers are also checked against a set of known reference articles, not retrieval metrics alone.

## Roadmap

- Phase 1 → Collect regulations, prepare documents
- Phase 2 → Chunking, embeddings, retrieval
- Phase 3 → LLM prompting, chatbot interface
- Phase 4 → Contract upload, analysis, comparison
- Phase 5 → Evaluation and results

Retrieval quality is settled before feature work begins. A polished interface over weak retrieval is worth nothing here.

## Status

In development.

## Data handling

Storing a contract is opt in. Users are asked first, and contracts are only saved if they agree. Saved contracts are what power comparison and salary benchmarking.

## Disclaimer

Sanad is an informational tool, not legal advice. Always verify against the official published regulations before acting on an answer.
