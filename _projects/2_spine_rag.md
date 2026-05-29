---
layout: page
title: Spine Oncology RAG Service
description: Production LLM/RAG system for spine tumor boards
img: assets/img/projects/spine-rag.jpg
importance: 2
category: current
---

{% include figure.liquid loading="eager" path="assets/img/projects/spine-rag.jpg" title="Spine oncology clinical context" class="img-fluid rounded z-depth-1" %}

A privacy-safe LLM/RAG service for spine tumor boards at Yale Neurosurgery. The system converts raw clinical context — imaging impressions, pathology reports, surgical history, guideline literature — into one-page briefs that accelerate oncologic decision-making.

**Early System.** Go-based orchestration and S3 streaming I/O behind FastAPI/Pydantic, deployed on Kubernetes (EKS) with Postgres/pgvector retrieval. Outputs FHIR-like structured JSON with inline citations to source documents. SRE-grade Grafana dashboards expose latency, reliability, and reasoning-trace observability so model behavior stays auditable.

**Role.** End-to-end ownership across model integration, evaluation tooling, retrieval iteration, deployment, and incident response. Cross-functional work spans neurosurgeons, data scientists, and engineers.

**Why it matters.** Most clinical LLM deployments stop at notebook demos. This one lives in an actual tumor board workflow, with the observability and structured outputs needed for guidance to be decision-ready rather than demo-grade.
