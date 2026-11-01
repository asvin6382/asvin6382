# Asvin Selvarajan

**Data Scientist · Machine Learning & GenAI · MLOps** — Tamil Nadu, India

I build machine-learning systems from raw data to a working service: features that respect time, models tested on
periods they have never seen, and APIs or live jobs that run them. About 3 years of experience, including 2.8 years
as a Data Scientist at HCL GUVI. I like explaining results in plain language, including the experiments that did not work.

Open to Data Scientist, ML Engineer and AI/ML Engineer roles · immediate joiner

---

## Research - R1 Breakout Ranker *(paper in preparation)*

**Question:** many intraday breakout signals fire on Indian stocks every morning, but taking all of them is close to a
coin flip. Can a model pick the ones that really run?

- **Approach:** a fixed rule finds breakout trades on 1,135 NSE stocks (5-minute data, 12 months, 8,344 trades);
  a gradient boosting model ranks them. Strict time split: 6 months to train, the next 6 months never seen.
- **Result:** on 4,374 unseen trades, the top 10% won **77%** of the time against a 50.5% base rate
  (Spearman IC **0.31**).
- **What the research showed:**
  - cash-flow features measured against each stock's own normal gave the biggest gain (IC 0.25 to 0.31)
  - a look-ahead leak had inflated results by 60%, and a strict causal check caught it
  - tree models beat GRU / TCN sequence models at this data size
  - chart images through a vision-language model did worse than simple handcrafted features
- Tracked in MLflow; runs live on AWS EC2. Code stays private until the paper is out.

**Roadmap to the paper**
- [ ] **Confidence intervals** - bootstrap ranges for the IC and the 77% win rate, to show the result is not luck
- [ ] **Several seeds** - retrain with different random seeds and report how much the result moves
- [ ] **Cost-adjusted returns** - subtract brokerage, taxes and slippage from every trade
- [ ] **Forward test** - score the next 6-12 months of new data with the model frozen as it is today, then walk-forward
- [ ] **Preprint**, then an updated version with the forward-test results

---

## Projects

### Real-time payments fraud detection → [payments-fraud-detection](https://github.com/asvin6382/payments-fraud-detection)
Fraud scoring on the **IEEE-CIS dataset (590k real card payments)**, trained on 4 months and tested only on the last month.
- Rebuilt 199k pseudo-customers (the data has no customer ID) and computed real-time window features: payments in the
  last 1 hour / 24 hours / 7 days, amount vs the customer's average, new device or e-mail.
- At the same alert volume (1% of payments): **83% precise, 24% of fraud caught** - against 16% and 4% for velocity rules.
  78% precise on customers never seen before.
- FastAPI service returns **approve / step-up (OTP) / block** with reasons; p95 latency 55 ms through the API.
- `XGBoost` `SHAP` `FastAPI` `pandas` `pytest`

### AI English-speaking coach - MVP for an EdTech startup → [case study](https://github.com/asvin6382/english-coach-mvp-case-study)
As the **core tech contributor** for a student-founded EdTech startup, I built and delivered the MVP of a
**voice-based AI English-speaking coach for Tamil-speaking learners** (Sep - Oct 2026).
- **The problem:** many Tamil speakers understand English but freeze when they have to speak it, and classes explain
  grammar in English - the language they are still learning.
- **What I built:** a voice-first coach that explains in Tamil and makes the learner *speak* English, one short step at
  a time. A LangGraph lesson flow runs teach → ask → listen → check → feedback.
- **Decisions by measurement:**
  - benchmarked LLM providers and chose one at **about Rs 0.02 per learner session, roughly 20x cheaper**
  - picked a cloud voice that replies in **under 1 second** inside the free tier
- **Testing before real users:** a simulator that acts as 5 different learners walked every lesson and
  **found 7 bugs before real users did**.
- `React` `FastAPI` `LangGraph` `LLM APIs` `speech-to-text` `text-to-speech` - the case study shows the method; the product code belongs to the startup.

---

## Work at HCL GUVI
Two systems I built in my Data Scientist role. The company's code and learner data stay with the company; to show how
they work, I rebuilt both from scratch on **synthetic data** (private repos, walkthrough on request).

### MentorMind - agentic AI assistant for learner doubts
An **agentic RAG assistant** that sits inside the learner doubt chatbot and decides how to handle each question.
- **LangGraph router** sends each doubt to the right sub-agent: answer it, reuse a past mentor solution, look up a
  session, guide a project with hints (never the full answer), or hand it to a mentor.
- **RAG with LlamaIndex + ChromaDB over three knowledge bases**, each chunk tagged with metadata:
  - **past mentor solutions** - tagged with course, topic, project and learner rating; searched within the learner's
    course, then re-ranked as 70% relevance + 30% rating, so well-rated answers come first
  - **hard doubts** that needed a live mentor call - a close match tells the agent to hand over early
  - **project briefs and solutions**, split step by step - tagged with project, step and `restricted`; the learner-facing
    search only sees briefs, while the hint agent reads the step's solution privately and gives a hint, never the answer
- **MCP server** gives the agents live session data (links, recordings) from a Google Sheet.
- Reads **error screenshots** (multimodal LLM); one swappable LLM client.
- `LangGraph` `LangChain` `MCP` `LlamaIndex` `ChromaDB` `FastAPI` `Docker`

### Learner bucketing and early warning
Weekly grouping of learners into Good / Average / Poor from attendance, practice and project progress, plus an
early-warning step so mentors reach struggling learners sooner. The rebuild compares models in MLflow, checks drift
(PSI) and serves weekly scores through FastAPI.

---

## Experience
| Role | Where | When |
|---|---|---|
| AI Engineer - Core Tech Contributor | Student-founded EdTech startup (MVP delivered) | Sep 2026 - Oct 2026 |
| Data Scientist (L&D) | HCL GUVI, Chennai | Dec 2023 - Aug 2026 |
| Data Science Intern | GUVI Geek Network | Oct 2023 - Dec 2023 |

## Tools
**ML:** scikit-learn, XGBoost, PyTorch, MLflow · **GenAI:** LangGraph, LangChain, RAG, ChromaDB, MCP ·
**Engineering:** Python, SQL, FastAPI, Docker, AWS (EC2, S3, Lambda), Git · **Data:** pandas, NumPy, Plotly, Power BI

## Contact
asvinselvarajan@gmail.com · [LinkedIn](https://linkedin.com/in/asvin-selvarajan-396377268)
