# Dual-RAG MAS Engine

## A research workspace for ingestion, retrieval, analysis, and collaboration

The Dual-RAG MAS Engine is a web-based research application designed to help teams turn paper collections into usable, queryable project knowledge. The current version combines structured upload workflows, hierarchical retrieval, figure understanding, artifact tracking, and collaborative Q&A inside a single interface.

This page is written for a user-facing audience. It highlights what the app does today, how it feels to use, and what makes the experience valuable in practice.

## What the current version enables

- Upload research papers into a namespace-based project workspace
- Ingest documents into a hierarchical retrieval pipeline for better context fidelity
- Extract figures from papers and generate figure-level analysis
- Store and browse project artifacts for each namespace
- Run Q&A over uploaded papers with source-aware retrieval
- Share namespaces and related resources with collaborators

## Product positioning

This is not just a chat layer over PDFs. It is a research workflow interface that organizes papers, figures, artifacts, and question answering around a project or namespace, so teams can move from raw documents to reusable knowledge.

## Core experience

### 1. Paper upload and ingestion

The application supports paper upload through a clean web interface with namespace targeting and ingestion controls. The upload flow is designed to feel operational rather than experimental: users select a project space, add one or more files, and trigger a processing pipeline that prepares the material for downstream retrieval and analysis.

**Why it matters**

- Reduces friction in getting papers into the system
- Organizes work by namespace rather than by loose file folders
- Creates the foundation for downstream Q&A, figure analysis, and artifact linking

**Suggested screenshot**

`[Screenshot: Upload or namespace ingestion screen showing drag-and-drop upload, namespace selector, and ingestion options]`

### 2. Hierarchical ingestion and retrieval

A major strength of the current version is its hierarchical ingestion-retrieval approach. Instead of treating a paper as a flat bag of chunks, the system preserves document structure and retrieves context at multiple levels. This improves answer quality, keeps evidence more coherent, and makes the resulting Q&A experience more aligned with how people actually read papers.

From a user perspective, this shows up as more grounded responses, better section-aware retrieval, and improved handling of paper-specific or method-specific questions.

**Why it matters**

- Improves context quality compared with naive chunk retrieval
- Supports more precise answers for methods, results, and paper-specific questions
- Helps preserve the meaning of tables, sections, and local document structure

**Suggested screenshot**

`[Screenshot: Q&A or research view showing an answer with retrieved sources or paper context]`

### 3. Figure extraction and analysis

The system can extract figures during ingestion and make them available through the interface. It also supports figure analysis, giving users a way to inspect visual content that would otherwise remain trapped inside PDFs. This is especially useful for technical papers where key findings live in plots, diagrams, and microscopy or process images rather than only in body text.

**Why it matters**

- Makes visual evidence visible and reusable
- Helps users inspect and compare figures without manually scanning full PDFs
- Expands retrieval beyond text-only workflows

**Suggested screenshot**

`[Screenshot: Figures tab or gallery view showing extracted figures and figure-level analysis]`

### 4. Namespace-level artifact database

Each namespace can serve as a project-level knowledge space, not just a paper repository. The current version includes artifact storage and browsing so users can track research assets such as models, datasets, force fields, configuration files, or related technical resources alongside the papers that describe them.

This turns the app into a more complete project memory layer.

**Why it matters**

- Keeps non-paper research assets attached to the right project context
- Supports reuse and traceability across a research workflow
- Encourages structured project organization rather than ad hoc storage

**Suggested screenshot**

`[Screenshot: Artifacts tab showing artifact cards, metadata, and namespace association]`

### 5. Q&A over project knowledge

The Q&A experience lets users ask natural-language questions against project content and receive answers grounded in retrieved paper context. Rather than forcing users to manually search across multiple documents, the system performs retrieval and synthesis on their behalf, making it easier to get to findings, methods, or comparative answers quickly.

This is one of the most important user-facing capabilities because it converts the system from a document store into an active research assistant.

**Why it matters**

- Speeds up literature review and evidence lookup
- Reduces manual cross-referencing across papers
- Makes technical project knowledge more accessible to collaborators

**Suggested screenshot**

`[Screenshot: Namespace Q&A tab with query input, answer panel, and cited/retrieved context]`

### 6. Shared projects and collaboration

The application includes sharing workflows for project resources, enabling collaborative use rather than single-user isolation. In practice, this supports a more team-oriented model in which namespaces and related materials can be shared with other users for viewing or collaboration.

This matters because research work is rarely solo. The app is being shaped as a shared workspace, not just a personal notebook.

**Why it matters**

- Supports collaborative project review
- Makes namespace-based knowledge easier to hand off or discuss
- Moves the product toward team use cases rather than single-user experimentation

**Suggested screenshot**

`[Screenshot: Share dialog showing permissions and resource sharing controls]`

## UI/UX highlights

The current interface emphasizes usability in a few important ways:

- A dashboard-and-namespace model that maps naturally to project work
- Deterministic admin flows for upload, organization, and browsing
- Research flows that reserve LLM usage for places where synthesis adds value
- Clear separation between operational tasks and exploratory Q&A
- Multi-tab namespace views that keep papers, figures, artifacts, and Q&A in one place

The result is a UI that feels more like a purpose-built research workspace than a generic AI demo.

## Why this product is compelling

Many research tools solve only one part of the problem: storage, search, chat, or reporting. The Dual-RAG MAS Engine is more compelling because it connects the full loop:

1. ingest papers,
2. preserve document structure,
3. retrieve context intelligently,
4. expose figures and artifacts,
5. answer questions in a project-aware workspace,
6. support collaboration around shared knowledge.

That combination makes it well suited for research groups, technical teams, and project environments where documents are only one part of the working knowledge base.

## Major future goals

The current version is already usable, but the roadmap is aimed at making the system more complete as a research workspace. The most important next steps are:

- **Table data ingestion:** extract tables as structured assets, not just text references, so users can retrieve and compare numeric results more directly
- **Review paper generation:** support higher-quality long-form review outputs that synthesize evidence across papers and can be stored, revisited, and shared
- **Claim-layer evidence tables:** add stronger structured evidence assembly with consensus and disagreement views across multiple papers
- **Cluster-aware retrieval for large collections:** improve performance and relevance as namespaces grow by routing queries through paper clusters
- **Richer multimodal ingestion:** expand support for tables, images, diagrams, and other non-text document elements as first-class knowledge objects
- **Deeper figure-and-report integration:** allow generated reviews and reports to incorporate figures and visual evidence more seamlessly
- **Stronger collaboration workflows:** continue improving shared project spaces, permissions, and resource handoff across teams

From a user perspective, these goals all point in the same direction: a system that does not just help answer isolated questions, but helps teams build, compare, synthesize, and communicate knowledge across a full research workflow.

## Short website version

The Dual-RAG MAS Engine is a research workspace for teams working with technical documents. It supports paper upload, hierarchical ingestion and retrieval, figure extraction and analysis, namespace-level artifact management, source-aware Q&A, and project sharing. The current UI is organized around namespaces so users can manage papers, visual evidence, artifacts, and answers inside a single project context.

## Optional homepage teaser

Turn paper collections into searchable project knowledge. The Dual-RAG MAS Engine combines hierarchical retrieval, figure understanding, artifact tracking, and collaborative Q&A in a web app designed for real research workflows.
