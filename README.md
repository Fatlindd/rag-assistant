# RAG Assistant

A Python-based Retrieval-Augmented Generation (RAG) assistant built as an AI Engineering project.

## Overview

RAG Assistant is a learning-oriented, production-minded project for building an AI assistant that answers questions using external documents and retrieved context.

Instead of relying only on the language model's internal knowledge, the application will retrieve relevant information from a knowledge base and provide that information to the model as context before generating an answer.

The project is being developed incrementally with a focus on clean architecture, maintainability, testing, evaluation, security, and practical AI Engineering principles.

## Goal

The goal of this project is to build a reusable RAG system capable of:

- ingesting external documents;
- preprocessing and splitting documents into chunks;
- generating embeddings;
- indexing document chunks;
- retrieving relevant context for a user query;
- generating grounded answers using retrieved context;
- providing source-aware responses;
- evaluating retrieval and answer quality;
- providing a foundation that can later be extended with an API or user interface.

## RAG Pipeline

The project will conceptually separate the main RAG responsibilities:

```text
Documents
    ↓
Ingestion
    ↓
Preprocessing
    ↓
Chunking
    ↓
Embeddings
    ↓
Indexing
    ↓
Retrieval
    ↓
Generation
    ↓
Evaluation
```

The exact technologies used for each stage will be selected based on project requirements rather than chosen in advance.

## Project Status

Current phase:

**Initial project setup and architecture preparation.**

Completed:

- Git repository initialization
- Python 3.12 environment setup
- Local virtual environment
- Python package structure
- Editable package installation
- Git ignore configuration
- Cursor ignore configuration
- Cursor Global User Rules
- Cursor Project Rules
- Python project metadata with `pyproject.toml`
- Basic project documentation

Not implemented yet:

- document ingestion
- preprocessing
- chunking
- embeddings
- vector storage
- retrieval
- LLM generation
- source citations
- evaluation
- API
- user interface

## Project Structure

```text
rag-assistant/
├── .cursor/
│   └── rules/
│       └── 00-project.mdc
│
├── data/
│   └── .gitkeep
│
├── docs/
│   └── .gitkeep
│
├── src/
│   └── rag_assistant/
│       └── __init__.py
│
├── tests/
│   └── .gitkeep
│
├── .cursorignore
├── .env.example
├── .gitignore
├── pyproject.toml
└── README.md
```

The local `.venv/` directory is intentionally not included in version control.

## Main Directories

### `src/rag_assistant/`

Contains the Python source code for the application.

This is the main Python package of the project.

Because the project is installed in editable mode, modules inside this package can be imported using:

```python
import rag_assistant
```

and later, for example:

```python
from rag_assistant.retrieval import retrieve
```

### `tests/`

Contains automated tests for application behavior.

Tests will be added as implementation begins.

### `docs/`

Contains project documentation such as:

- requirements;
- architecture documentation;
- technical decisions;
- RAG pipeline documentation;
- implementation notes.

### `data/`

Contains local data used by the RAG system.

Private or sensitive documents must not be committed to Git.

The project also reserves:

```text
data/private/
```

for private local documents that should not be used as Cursor codebase context.

### `.cursor/rules/`

Contains project-specific Cursor instructions.

The current base rule is:

```text
.cursor/rules/00-project.mdc
```

It defines project-level engineering principles, development workflow, RAG responsibilities, runtime configuration, testing expectations, and change-scope rules.

## Requirements

- Python 3.12+
- Git
- Python virtual environment support
- pip

The project currently targets Python 3.12.

The development environment used during initial setup is:

```text
Python 3.12.14
```

## Local Development Setup

### 1. Clone the repository

```bash
git clone <repository-url>
cd rag-assistant
```

If the repository has not yet been published remotely, open the local project directory directly.

### 2. Create a virtual environment

```bash
python3.12 -m venv .venv
```

### 3. Activate the virtual environment

On macOS or Linux:

```bash
source .venv/bin/activate
```

Verify that the correct Python interpreter is active:

```bash
which python
```

The path should point to:

```text
rag-assistant/.venv/bin/python
```

### 4. Verify the Python version

```bash
python --version
```

Expected:

```text
Python 3.12.x
```

### 5. Install the project in editable mode

```bash
python -m pip install -e .
```

This installs the `rag-assistant` package inside the active virtual environment while keeping it connected to the source code under:

```text
src/rag_assistant/
```

### 6. Verify the package installation

```bash
python -c "import rag_assistant; print(rag_assistant.__file__)"
```

The output should point to:

```text
src/rag_assistant/__init__.py
```

## Editable Installation

The project uses an editable Python installation during development:

```bash
python -m pip install -e .
```

Editable mode means that the installed package remains connected to the source code.

Conceptually:

```text
.venv
  │
  └──────→ src/rag_assistant/
```

Changes made inside:

```text
src/rag_assistant/
```

become available immediately without reinstalling the project after every code change.

## Python Package

The main Python package is:

```text
rag_assistant
```

Its source location is:

```text
src/rag_assistant/
```

The package currently contains:

```text
src/rag_assistant/
└── __init__.py
```

Additional modules will be introduced only when required by the approved architecture.

## Configuration

Environment-specific values and secrets must not be hardcoded in source code.

Examples include:

- API keys;
- database URLs;
- vector database credentials;
- model provider configuration;
- authentication secrets.

A local `.env` file may later be used for environment-specific values.

The real `.env` file must not be committed to Git.

The repository contains:

```text
.env.example
```

which will serve as a safe template showing which environment variables are required without containing real secret values.

## Dependency Management

Project metadata and runtime dependencies are managed through:

```text
pyproject.toml
```

The project currently has:

```toml
dependencies = []
```

because the RAG technology stack has not yet been finalized.

Dependencies will be introduced only when required by an approved implementation decision.

The current build configuration uses:

```toml
[build-system]
requires = ["setuptools"]
build-backend = "setuptools.build_meta"
```

Package discovery is configured for the `src` layout:

```toml
[tool.setuptools.packages.find]
where = ["src"]
```

## Build System

The project uses `setuptools` as its Python build backend.

`setuptools` is responsible for helping Python tooling understand how the project should be packaged and installed.

`pip` is responsible for installing the project and its declared dependencies.

Conceptually:

```text
pyproject.toml
      ↓
pip
      ↓
setuptools
      ↓
src/rag_assistant/
      ↓
installed Python package
```

## Git

The project uses Git for version control.

The main development branch is:

```text
main
```

Files and directories that should not be committed are configured in:

```text
.gitignore
```

Examples include:

- `.venv/`
- `.env`
- Python cache files
- test caches
- build artifacts
- macOS metadata

## Cursor Configuration

Cursor is configured as an AI-assisted development environment for this project.

### Global User Rules

Global User Rules define how Cursor should generally work across projects, including principles such as:

- understand requirements before coding;
- inspect existing code first;
- prefer focused changes;
- avoid unrelated modifications;
- test behavioral changes;
- review final changes.

### Project Rules

Project-specific rules are stored under:

```text
.cursor/rules/
```

The current core rule is:

```text
.cursor/rules/00-project.mdc
```

It is configured as:

```text
Always Apply
```

so it is included in Cursor conversations for this repository.

### Cursor Ignore

Cursor-specific exclusions are configured in:

```text
.cursorignore
```

Current exclusions include:

```text
data/private/
vector_store/
```

These locations are intended for private documents or generated vector data that should not be part of normal Cursor codebase context.

## Engineering Principles

The project follows several core engineering principles:

- prefer simple and explicit implementations;
- avoid unnecessary abstractions;
- keep modules focused on a single responsibility;
- maintain separation of concerns;
- avoid unnecessary dependencies;
- never hardcode secrets or credentials;
- make incremental changes;
- keep diffs focused;
- preserve existing behavior unless requirements explicitly change it;
- add or update tests when behavior changes;
- validate changes before considering work complete.

## RAG Design Principles

The major RAG responsibilities should remain conceptually separated:

- document ingestion;
- preprocessing;
- chunking;
- embeddings;
- indexing;
- retrieval;
- generation;
- evaluation.

Unrelated RAG responsibilities should not be combined into one large module.

This does not mean that every responsibility must immediately become a separate package or directory.

The architecture will evolve incrementally as project requirements become clearer.

## Architecture Decisions

Major technology choices have intentionally not been finalized yet.

Future decisions include:

- LLM provider;
- embedding model;
- vector database;
- RAG framework versus custom implementation;
- document parsing strategy;
- chunking strategy;
- retrieval strategy;
- reranking strategy;
- prompt construction;
- evaluation framework;
- observability;
- API framework;
- user interface.

These decisions should be made based on requirements rather than selecting technologies first.

Significant architectural decisions should be documented before implementation.

## Testing

Automated tests will live inside:

```text
tests/
```

Testing will evolve together with the implementation.

Expected future testing areas include:

- document ingestion;
- preprocessing;
- chunking behavior;
- embedding integration;
- retrieval correctness;
- configuration;
- error handling;
- RAG pipeline integration;
- source grounding;
- evaluation behavior.

Relevant tests should be run before considering implementation work complete.

## Evaluation

RAG evaluation will be treated as a first-class part of the project rather than an afterthought.

Future evaluation may include:

- retrieval relevance;
- context precision;
- context recall;
- groundedness;
- answer relevance;
- citation correctness;
- latency;
- cost.

The final evaluation approach will be selected after the initial RAG architecture is defined.

## Security

The repository must never contain:

- API keys;
- passwords;
- access tokens;
- private credentials;
- production secrets;
- sensitive private documents.

Secrets should be provided through environment variables or an appropriate secret-management system.

Private RAG documents should remain outside version control and should be excluded from Cursor context where appropriate.

## Development Workflow

For non-trivial changes, the preferred workflow is:

```text
Requirement
    ↓
Understand
    ↓
Inspect existing code
    ↓
Plan
    ↓
Identify affected files
    ↓
Consider risks and edge cases
    ↓
Implement incrementally
    ↓
Add or update tests
    ↓
Run validation
    ↓
Review diff
    ↓
Commit
```

Cursor is used as an AI-assisted engineering tool.

Architecture decisions, testing, code review, and final validation remain explicit parts of the development process.

## Git Workflow

Before committing changes:

```bash
git status
```

Review staged files:

```bash
git diff --cached --stat
```

Review the complete staged diff:

```bash
git diff --cached
```

Only approved changes should be committed.

## Roadmap

The current expected development roadmap is:

1. Define functional requirements.
2. Define non-functional requirements.
3. Design the initial RAG architecture.
4. Select the first supported document format.
5. Implement document ingestion.
6. Implement preprocessing.
7. Implement chunking.
8. Select an embedding model.
9. Introduce vector indexing.
10. Implement retrieval.
11. Add LLM-based generation.
12. Add source grounding and citations.
13. Add automated RAG evaluation.
14. Add observability and logging.
15. Add an API layer.
16. Add a user interface if required.
17. Improve retrieval quality and performance.
18. Prepare the project for deployment.

The roadmap may evolve as requirements and architecture decisions become clearer.

## License

No license has been selected yet.