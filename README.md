# Intelligent APP Classification Agent

A multi-agent, high-concurrency system for end-to-end APK automated review, combining static analysis, cloud phone dynamic testing, traffic capture, and multi-modal classification.

---

## System Architecture & Workflow
A StateGraph-based pipeline built with LangGraph, replacing hard-coded scripts with conditional edges to handle retries, degraded modes, and complex branching logic.
![work_flow](https://github.com/lichong-007/Intelligent-APP-Classification-Agent-/blob/main/assets/work_flow.png)


---

## 1. Batch Task Management & Concurrency Control
Celery + Redis async queue for distributing bulk APK tasks, with multi-worker parallel processing, cloud phone rate limiting, and retry mechanisms to support large-scale sample batch runs.



---

## 2. Static & Multi-modal Feature Extraction
Extracts static metadata (package name, certificate, MD5) and visual features (screenshots). Supports degraded classification when no traffic data is available.



---

## 3. Traffic Capture & URL Analysis
Performs automated traffic capture during dynamic testing, extracting URLs and network behavior to feed into multi-modal classification.



---

## 4. Human-in-the-loop Review via MCP
High-confidence results are written directly to PostgreSQL. Low-confidence cases are marked for human review, with MCP tools to query pending tasks and update labels without re-running the pipeline.



---

## Tech Stack
- **Orchestration**: LangGraph (StateGraph + conditional edges)
- **Async & Concurrency**: Celery, Redis
- **Storage**: PostgreSQL (MCP-managed human review results)
- **Dynamic Testing**: Cloud Phone / ADB automation
- **Classification**: Rule engine + LLM multi-modal fusion
- **Scaling**: Docker-based elastic worker scaling

## Core Capabilities
- **End-to-end Automated Review**: From APK upload to multi-label classification without manual intervention
- **Resilient Workflow**: Native support for retries, timeouts, and degraded modes (e.g., no traffic → static+visual only)
- **High Throughput**: Async task queue + parallel workers to handle large-scale APK batches
- **Human-in-the-loop Closed Loop**: MCP-enabled review process to improve classification accuracy and reduce manual effort
