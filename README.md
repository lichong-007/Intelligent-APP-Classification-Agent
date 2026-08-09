# Intelligent APP Classification Agent

A high-concurrency APK automated review system that uses Celery and Redis for batch task scheduling, LangGraph for per-app workflow orchestration, and combines cloud-phone probing, pcap traffic analysis, rule extraction, and multi-modal LLM classification.

---

## System Architecture & Workflow
A StateGraph-based pipeline built with LangGraph, replacing hard-coded scripts with conditional edges to handle retries, degraded modes, and complex branching logic.
![flow1](https://github.com/lichong-007/Intelligent-APP-Classification-Agent/blob/main/assets/flow1.png)


---

## 1. Static Feature Extraction
Extracts static metadata (package name, certificate, MD5) 
![static_report](https://github.com/lichong-007/Intelligent-APP-Classification-Agent/blob/main/assets/static_report.png)

---

## 2. Dynamic Screenshot Extraction
Uses ADB to capture and store app screenshots. Supports classification when traffic data is available.

![app_screenshort](https://github.com/lichong-007/Intelligent-APP-Classification-Agent/blob/main/assets/app_screenshort.png)

---

## 3. Extracting host and URL information in pcap
Extracting host and URL information from PCAP traffic captures during dynamic testing for multi-modal classification.
![parse_pcap](https://github.com/lichong-007/Intelligent-APP-Classification-Agent/blob/main/assets/parse_pcap.png)

---


## 4. Structured Dynamic Testing Results
Standardized structured output from APK dynamic analysis, including package name, version, certificates, and multi-modal classification result.
![dynamic_result](https://github.com/lichong-007/Intelligent-APP-Classification-Agent/blob/main/assets/dynamic_result.png)



---

## 5. Final Classification Results Web Dashboard
A web interface displaying the final multi-modal classification results, including app metadata, MD5, category labels, and review status, enabling quick lookup and human-in-the-loop management.
![app_classification(1)](https://github.com/lichong-007/Intelligent-APP-Classification-Agent/blob/main/assets/app_classification(1).png)


---

## Core Capabilities
- **Batch APP Detection Pipeline**: Processes large-scale APP batches through Celery and Redis, with each APP handled independently by a LangGraph workflow.
- **Dynamic Traffic-based Rule Extraction**: Uses cloud-phone probing and pcap traffic capture to extract detection rules through scripts, then checks whether the rules match the existing rule library.
- **Multi-modal APP Classification**: Uses an LLM to classify APPs based on certificates, screenshots, icons, package information, and extracted rule URLs.
- **Review and Failure Tracking**: Records cases with no extracted rules, unstable rules, or execution failures for later manual review and troubleshooting.



## Tech Stack
- **Orchestration**: LangGraph (StateGraph + conditional edges)
- **Async & Concurrency**: Celery, Redis
- **Storage**: PostgreSQL 
- **Dynamic Testing**: Cloud Phone / ADB automation
- **Classification**: Rule engine + LLM multi-modal fusion
