# Intelligent APP Classification Agent

A multi-agent, high-concurrency system for end-to-end APK automated review, combining static analysis, cloud phone dynamic testing, traffic capture, and multi-modal classification.

---

## System Architecture & Workflow
A StateGraph-based pipeline built with LangGraph, replacing hard-coded scripts with conditional edges to handle retries, degraded modes, and complex branching logic.
![work_flow](https://github.com/lichong-007/Intelligent-APP-Classification-Agent-/blob/main/assets/work_flow.png)


---

## 1. Static Feature Extraction
Extracts static metadata (package name, certificate, MD5) 
![static_report](https://github.com/lichong-007/Intelligent-APP-Classification-Agent-/blob/main/assets/static_report.png)

---

## 2. Dynamic Screenshot Extraction
Extracts dynamic features (screenshots). Supports degraded classification when no traffic data is available.

![app_screenshort](https://github.com/lichong-007/Intelligent-APP-Classification-Agent-/blob/main/assets/app_screenshort.png)

---

## 3. Extracting host and URL information in pcap
Extracting host and URL information from PCAP traffic captures during dynamic testing for multi-modal classification.
![parse_pcap](https://github.com/lichong-007/Intelligent-APP-Classification-Agent-/blob/main/assets/parse_pcap.png)

---


## 4. Structured Dynamic Testing Results
Standardized structured output from APK dynamic analysis, including package name, version, certificates, and multi-modal classification.
![dynamic_result](https://github.com/lichong-007/Intelligent-APP-Classification-Agent-/blob/main/assets/dynamic_result.png)



---

## 5. Final Classification Results Web Dashboard
A web interface displaying the final multi-modal classification results, including app metadata, MD5, category labels, and review status, enabling quick lookup and human-in-the-loop management.
![app_classification(1)](https://github.com/lichong-007/Intelligent-APP-Classification-Agent-/blob/main/assets/app_classification(1).png)
![app_classification(2)](https://github.com/lichong-007/Intelligent-APP-Classification-Agent-/blob/main/assets/app_classification(2).png)


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
- **Resilient Workflow**: Native support for retries, timeouts, and degraded modes 
- **High Throughput**: Async task queue + parallel workers to handle large-scale APK batches
- **Human-in-the-loop Closed Loop**: MCP-enabled review process to improve classification accuracy and reduce manual effort
