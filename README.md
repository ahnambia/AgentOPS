# AgentOPS
A command-line “agent orchestration” tool that lets non-technical users assemble, run, and monitor multimodal AI pipelines (e.g., retrieval, summarization, decision agents) with a plugin-based architecture. 

AgentOps — System Blueprint
Architecture at a glance

          ┌────────────┐      YAML DAG         ┌───────────────┐
CLI (Typer)─▶ Pipeline  ├─────(parse/validate)─▶ Orchestrator   │
          └─────┬──────┘                       │ (Engine)       │
                │                               └─────┬─────────┘
                │                                   (enqueue/run)
         MLflow client                              │
     (params/metrics/artifacts)                     ▼
        ┌───────────────┐                  ┌────────────────────┐
        │     MLflow    │◀────────────────▶│ Workers (RQ/Celery)│
        │ (Postgres+S3) │    run logs/art  │ run node tasks      │
        └──────┬────────┘                  └──────┬──────────────┘
               │                                   │
               │                         ┌─────────▼─────────┐
        ┌──────▼─────┐   embed/query     │  Vector DB (Qdrant)│
        │  Prom+Graf │◀──────────────────▶                  │
        │  Dash+Alrt │    runtime metrics └─────────▲────────┘
        └──────┬─────┘                               │
               │                                     │
               ▼                                     │
      ┌────────────────┐                    ┌────────┴─────────┐
      │ Basic Web UI   │◀─────read-only────▶│  Redis (cache +  │
      │ (FastAPI)      │    run history     │  RQ broker)      │
      └────────────────┘                    └───────────────────┘

