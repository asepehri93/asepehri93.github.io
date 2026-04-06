# Dual-RAG MAS Engine

## Technical Report

### A multi-agent research system for structured ingestion, hierarchical retrieval, and project-aware knowledge work

## Executive summary

The Dual-RAG MAS Engine is a full-stack research application I designed and implemented to turn technical paper collections into usable, project-scoped knowledge systems. It combines a web UI, an API layer, a namespace-based vector retrieval system, a graph-backed knowledge layer, and a multi-agent orchestration workflow for question answering and analysis.

The project is important to me as both a product and an engineering artifact. It demonstrates how I think about applied AI systems beyond prompt wiring: system boundaries, retrieval quality, workflow design, observability, failure handling, user experience, and the tradeoff between deterministic software and LLM-powered reasoning.

At its current stage, the system supports:

- paper upload and ingestion into project namespaces,
- hierarchical retrieval for better context fidelity,
- figure extraction and optional figure analysis,
- namespace-level artifact storage and browsing,
- source-aware Q&A over project knowledge,
- sharing workflows for collaborative use,
- a web interface built for actual usage rather than notebook-only experimentation.

## The problem it addresses

Technical teams and research groups often work across PDFs, figures, methods sections, datasets, notes, and project-specific assets. Traditional document search is too shallow, while many AI interfaces flatten everything into a generic chat experience that loses structure, provenance, and workflow context.

I built this system to address a more realistic problem:

How do you create a research tool that preserves document structure, supports higher-quality retrieval, keeps non-paper assets in the same knowledge environment, and exposes the result through a usable product surface?

## What makes this system notable

### 1. Dual-layer knowledge design

The system uses a dual-layer retrieval architecture:

- **Layer 1:** namespace-scoped vector retrieval for project isolation and paper-specific access
- **Layer 2:** graph-backed knowledge retrieval for broader relationships and cross-document context

This matters because project work often needs both local precision and global structure. Namespace isolation keeps work organized and relevant. The graph layer enables richer relationship-aware exploration when the use case calls for it.

### 2. Hierarchical retrieval rather than flat chunk retrieval

One of the most important technical choices in the system is hierarchical retrieval. Instead of relying only on small chunks, the ingestion and retrieval pipeline preserves parent-child structure and supports section-aware access patterns.

This improves several failure modes common in RAG systems:

- answers based on incomplete chunk fragments,
- loss of section context,
- weak handling of methods or result-specific questions,
- brittle retrieval when the right evidence spans adjacent chunks.

The result is a system that is more likely to retrieve context in the way a human reader would want it assembled.

### 3. Multi-agent orchestration with explicit roles

The project is not a single-model wrapper. It uses a multi-agent design with specialized responsibilities across orchestration, planning, retrieval, writing, auditing, and administrative workflows.

Core roles include:

- **Orchestrator:** request entry point and workflow routing
- **Planner:** query decomposition and task shaping
- **Librarian:** retrieval specialist across vector and graph layers
- **Writer:** answer synthesis and output formation
- **Auditor:** quality checks and evaluation-oriented safeguards

This separation is useful not because “multi-agent” is fashionable, but because complex AI workflows benefit from explicit boundaries. It makes the system easier to reason about, instrument, and improve.

### 4. Product-aware AI design

A key design principle in the web application is reserving LLM usage for places where it adds real value. Administrative workflows such as namespace creation, browsing, uploads, and listings are deterministic. LLM-powered logic is used where synthesis, interpretation, or analysis is genuinely needed.

That separation has practical benefits:

- lower cost,
- better predictability,
- easier debugging,
- clearer user expectations.

This is the kind of decision I consider central to production-minded AI engineering.

## System architecture

At a high level, the system includes:

- **Frontend:** Next.js application for authentication, namespaces, ingestion, figures, artifacts, reports, and Q&A
- **Backend:** FastAPI service exposing deterministic admin routes and LLM-powered research routes
- **Vector layer:** namespace-aware document storage and retrieval
- **Graph layer:** Neo4j-backed relationship and context retrieval
- **Orchestration layer:** LangGraph-based workflow across specialized agents
- **Storage layer:** SQLite/Postgres-ready app data plus file-backed research assets

This architecture was chosen to keep the user experience responsive while preserving separation between application concerns, retrieval logic, and LLM-driven reasoning.

## Methodologies and technical strategies

### Structured ingestion

The ingestion pipeline does more than store PDFs. It parses documents, supports figure extraction, and prepares them for downstream retrieval with structural awareness. The goal is to make documents usable as project knowledge, not merely indexable text blobs.

### Section-aware retrieval

Queries are not always generic. Some target methods, some target findings, and some are paper-specific. The system uses retrieval strategies that can adapt based on query type, allowing better alignment between the question being asked and the context that gets assembled.

### Figure extraction and analysis

Technical papers often contain critical evidence in visual form. The system therefore treats figures as first-class assets. During ingestion, figures can be extracted and surfaced in the UI, and vision-based analysis can be applied to generate figure-level descriptions and concepts.

This expands the system beyond text-only retrieval and reflects a more realistic treatment of scientific and technical content.

### Namespace-scoped artifacts

A research system should not stop at papers. I added artifact handling so each namespace can also contain project-relevant technical assets such as datasets, models, force fields, or related resources. This makes the namespace concept closer to a working project environment than a document folder.

### Quality and regression safeguards

The project includes explicit work on QA quality and failure diagnosis. In particular, I added diagnostic logic to distinguish retrieval failures from answer-generation failures and introduced a regression invariant for a specific high-value failure mode: when explicit numeric evidence is present in context, the system should not answer as if the quantity was “not reported.”

That work reflects an engineering mindset I care about strongly: AI quality should be monitored with concrete behavioral checks, not only anecdotal prompting tweaks.

### Observability and traceability

The system includes timing logs, correlation IDs, and improved diagnostics across retrieval and processing flows. This is important in multi-stage AI systems because many failures are pipeline failures rather than model failures. Good observability makes iteration substantially faster and safer.

## Technical novelty and differentiators

The project’s novelty is not in inventing a new foundation model. It is in how multiple techniques are combined into a coherent, usable system:

- dual-layer retrieval that balances local namespace precision with broader graph context,
- hierarchical parent-document retrieval to preserve structure,
- multi-agent workflow design with explicit responsibilities,
- figure-aware knowledge handling,
- artifact-aware project organization,
- deterministic vs. LLM workflow separation,
- regression-oriented safeguards for answer quality,
- a real product surface rather than a notebook-only prototype.

Taken together, these choices produce a system that is more credible, more inspectable, and more useful than a basic “chat with PDFs” implementation.

## Engineering decisions that matter to industry

From an industry perspective, the most relevant aspects of this work are:

- **Architecture discipline:** clear separation of frontend, API, orchestration, retrieval, and storage concerns
- **Applied AI realism:** use of LLMs where helpful, deterministic code where preferable
- **Retrieval quality focus:** attention to context fidelity and failure analysis
- **Observability:** correlation IDs, timing logs, and diagnostics for debugging multi-step systems
- **Extensibility:** namespaces, agents, routes, and services are structured for growth
- **User-facing delivery:** the system is accessible through a web product, not only through scripts

This is the kind of project that demonstrates end-to-end ownership: not only building a model interface, but shaping the surrounding software system so the AI behavior becomes useful and operational.

## Audience-specific relevance

### For hiring managers

This project shows that I can operate across the full stack of modern AI product development:

- backend and API design,
- frontend product delivery,
- retrieval and knowledge system design,
- LLM workflow engineering,
- debugging and quality control,
- translating technical capability into a usable application.

### For engineering leaders

The system demonstrates judgment in system design, especially around retrieval quality, decomposition of AI workflows, and the boundary between model-driven and deterministic behavior.

### For product and applied AI teams

The project is a concrete example of how to turn AI capability into software that fits an actual workflow. The emphasis is not on novelty theater. It is on usability, trustworthiness, and engineering clarity.

## Current status

The project is an active, working implementation with a web UI and core feature set in place. It is not presented as a finished enterprise platform, but as a serious, functioning system that already demonstrates:

- project-scoped knowledge organization,
- hierarchical retrieval,
- figure and artifact support,
- agentic Q&A workflows,
- collaboration-oriented sharing patterns,
- quality instrumentation and regression thinking.

That combination is exactly why I consider it representative of the kind of work I want to do professionally.

## Future goals and roadmap direction

The next phase of the project is not just about adding more features. It is about increasing the structural depth of the knowledge system and improving how evidence is assembled, compared, and turned into research outputs.

The major roadmap items are:

- **Table data ingestion and structured table retrieval:** move beyond table references toward extracting table content as a retrievable, structured knowledge source for numeric and comparative questions
- **Review paper generation:** extend the system from Q&A and reports toward more robust review-paper style synthesis across paper sets, including support for stored long-form outputs
- **Claim-layer evidence tables:** introduce stronger structured evidence assembly with consensus clusters, disagreement clusters, and gap detection for multi-paper reasoning
- **Cluster-aware routing for large namespaces:** use clustering and cluster-level routing to keep retrieval scalable and relevant as collections grow
- **Richer multimodal document understanding:** treat figures, tables, diagrams, and other non-text elements as more complete first-class retrieval objects
- **Tighter report, citation, and visual integration:** improve how generated outputs incorporate figures, evidence structures, and source grounding
- **Stronger collaboration and project sharing:** continue evolving the system from a single-user tool into a more complete shared research workspace

From a technical standpoint, these goals are appealing because they build on the existing architecture rather than replacing it. The current system already has the right abstractions for namespaces, orchestration, structured retrieval, and evidence-aware quality control. The roadmap extends those abstractions into more capable research synthesis and collaboration workflows.

## Closing statement

The Dual-RAG MAS Engine is the strongest kind of technical project for me to present in a hiring context because it combines AI, systems design, product thinking, and implementation discipline in one artifact. It reflects how I approach real-world engineering problems: define the workflow, preserve structure, build clear system boundaries, make quality observable, and deliver the result through a usable interface.

If needed, this document can be adapted into a shorter portfolio page, a resume-linked project summary, or a PDF case study for applications.
