# AgentOPS
A command-line “agent orchestration” tool that lets non-technical users assemble, run, and monitor multimodal AI pipelines (e.g., retrieval, summarization, decision agents) with a plugin-based architecture. 

## Architecture at a glance

- **CLI (Typer)**: Command-line interface that accepts user commands and translates them into YAML DAGs.
- **Pipeline**: A DAG that defines the structure of the AI pipeline.
- **Orchestrator (Engine)**: The core component that parses, validates, and orchestrates the pipeline execution.
- **MLflow client**: A client that interacts with MLflow (a platform for managing the machine learning lifecycle).
- **MLflow (Postgres+S3)**: Stores parameters, metrics, and artifacts of the MLflow runs.
- **Workers (RQ/Celery)**: A job queue and task execution engine that runs node tasks.
- **Vector DB (Qdrant)**: Stores embeddings and indexes for vector search.
- **Prom+Graf**: Monitors runtime metrics and provides a basic web UI.
- **Basic Web UI (FastAPI)**: A read-only web interface for viewing run history.
- **Redis (cache + RQ broker)**: Caches data and acts as a message broker for RQ.

