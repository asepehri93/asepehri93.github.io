# SkyLune Dream Interpretation Engine — Technical Brief

**Audience:** Engineering leadership, hiring managers, technical partners  
**Purpose:** Communicate system design, rigor, and novelty at a level appropriate for evaluation and planning — **not** a build specification.  
**Last updated:** April 2026  

---

## 1. Summary

The SkyLune dream interpretation engine is a **server-orchestrated, multi-stage analysis pipeline** that pairs **large language models** with **structured methodology**, **retrieval-augmented context**, and **explicit safety and epistemic guardrails**. It powers the **Dream Work** experience inside the SkyLune iOS app: users move through a guided flow (dream text, emotional scenes, personal associations) and receive **multi-hypothesis interpretations** and **integration-oriented outputs**, rather than a single “dream dictionary” answer.

The design intent is **faithful to Jungian clinical craft** (personal meaning first, provisional language, multiple valid readings) while remaining **operable as production software** (session lifecycle, API boundaries, degradable dependencies).

---

## 2. Architectural stance

### Orchestrated multi-agent workflow

Analysis is not a one-shot prompt. A **central orchestrator** advances a **discrete session model** through ordered stages that mirror how depth-oriented dream work is actually done: stabilize the narrative, attend to feeling-tone, anchor symbols in **the dreamer’s associations**, then bring in curated conceptual material only as **support**, not as authority.

Specialized **agents** own slices of that pipeline (intake and structure, affect, associations, pattern detection, interpretation synthesis, optional amplification, integration planning, quality review, narrative summarization). Each stage has a **narrow contract** (inputs/outputs in structured form), which keeps behavior **testable**, **auditable**, and **evolvable** without rewriting a monolith.

### Dual retrieval (“dual-RAG”)

The engine combines **semantic retrieval** over multiple **curated knowledge channels**—conceptual material, exemplar cases, and procedural “how to work this dream” guidance—so that generated text is **grounded** in an internal library aligned with the chosen methodology, not only in the model’s pretrained prior. Retrieval is **selective**: it informs hypotheses and framing without collapsing the dream into generic archetype talk.

This is a deliberate **systems** choice: separate **what to know** (knowledge bases) from **how to reason stepwise** (agents + orchestration) from **how to speak** (LLM generation under policy).

### Methodology and policy layer

Interpretation is constrained by **injected axioms and policies** (e.g., multiple valid interpretations, non-diagnostic stance, careful use of archetypal vocabulary). That layer is part of the **product ethics** as much as the architecture: the system is designed to **avoid false certainty** and to privilege the user’s own material.

---

## 3. Technical strengths demonstrated

| Area | What it shows |
|------|----------------|
| **Systems design** | Explicit state machine + orchestrator; separation of retrieval, generation, and session persistence; clear API surface for a mobile client. |
| **ML product engineering** | LLMs used where they excel (language, synthesis) and **structured stages** where reliability and UX matter; hybrid of symbolic workflow + neural generation. |
| **RAG done with intent** | Multi-source retrieval tied to **role-specific** use (facts vs cases vs instructions), not a single blob of “context.” |
| **Safety & governance** | Crisis/safety awareness in the pipeline; archetype terminology handled with **user-context sensitivity** where relevant. |
| **Quality/cost awareness** | Hybrid strategies (e.g., deterministic post-processing for known failure modes) to reduce **bad outputs and wasted tokens** without adding redundant model calls. |
| **Operations** | Containerized service, cloud deployment, health endpoints; tolerant fallbacks when optional infrastructure (cache/DB) is absent. |
| **Cross-stack ownership** | End-to-end thinking: **iOS client** session cache, encoding alignment with server models, timeouts and degraded modes appropriate for mobile networks. |

---

## 4. Novelty and creativity (framed for a technical reader)

- **Epistemic design:** The product choice to ship **several hypotheses** plus **integration steps** is an engineering reflection of a clinical stance — implemented as **data structures and UI contracts**, not only copywriting.
- **Personal associations as first-class data:** The pipeline is built so **user-supplied associations** drive interpretation **before** archetypal amplification dominates — reversing the typical “AI dream app” pattern.
- **Depth modes:** Analysis depth is **parameterized** (e.g., symbol count, optional amplification), mapping product tiers to **compute and retrieval cost** without forking unrelated codebases.
- **Grounded creativity:** “Creativity” here is **constrained generation** — poetic, humane output within **retrieve-then-reason** boundaries, not unconstrained storytelling.

---

## 5. Client integration (high level)

The iOS application maintains a **local-first session artifact** synchronized with the engine over HTTPS. The client implements **resilient UX**: extended timeouts for LLM-heavy steps, **graceful degradation** when the network or server is slow, and **schema-level compatibility** (e.g., naming conventions across Swift and Python stacks). This is standard distributed-systems hygiene applied to a **non-trivial UX flow** (multi-screen ritual, not a single form post).

---

## 6. Boundaries of this document

This brief **does not** include: full state diagrams, prompt libraries, knowledge base contents, embedding indices, or step-by-step reproduction procedures. Those remain **internal engineering artifacts** for maintainers.

For **implementation-level** documentation (API routes, agent APIs, setup), authorized engineers should use the repository’s **`dream_engine/docs/`** tree and operational notes alongside **`docs/DEPLOYMENT.md`** for deployment context.

---

## 7. One-line positioning

**A methodology-first, retrieval-grounded, multi-agent dream analysis engine built for accountable LLM use in a consumer ritual product — designed for depth, humility, and operability, not for black-box one-shot answers.**
