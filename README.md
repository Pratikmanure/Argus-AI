# ARGUS Defense Core (ADC)

> **AI-Orchestrated Multi-Agent Cyber Defense Framework for Explainable,
> Risk-Aware and Confidence-Gated Threat Response**

ARGUS Defense Core (ADC) is a research-oriented cybersecurity framework
designed to coordinate multiple specialized security agents under a
central AI decision layer.

ARGUS collects security evidence, analyzes threats through specialized
agents, fuses their findings, calculates risk, explains decisions, and
determines whether a response can be safely automated or should be
escalated to a human analyst.

> **Core idea:** ARGUS does not only ask *"Is this a threat?"* --- it
> also asks *"Is the evidence strong enough for us to trust the
> decision?"*

## Table of Contents

-   [Project Overview](#project-overview)
-   [Problem Statement](#problem-statement)
-   [Objectives](#objectives)
-   [Architecture](#architecture)
-   [Specialized Agents](#specialized-agents)
-   [ARGUS Defense Core](#argus-defense-core)
-   [Confidence-Gated Decision
    Pipeline](#confidence-gated-decision-pipeline)
-   [AI/ML Pipeline](#aiml-pipeline)
-   [Datasets](#datasets)
-   [Technology Stack](#technology-stack)
-   [Prototype Scope](#prototype-scope)
-   [Repository Structure](#repository-structure)
-   [Evaluation](#evaluation)
-   [Research Direction](#research-direction)
-   [Development Roadmap](#development-roadmap)
-   [Team Responsibilities](#team-responsibilities)
-   [Project Status](#project-status)
-   [Future Work](#future-work)
-   [Security and Safety](#security-and-safety)
-   [License](#license)

## Project Overview

ARGUS is an AI-orchestrated multi-agent cyber-defense framework.
Specialized agents investigate different security domains while the
central Defense Core correlates their findings and coordinates
decisions.

The intended workflow is:

**Detect → Investigate → Fuse → Assess → Explain → Trust → Respond →
Learn**

ARGUS is not intended to replace antivirus, IDS, EDR, SIEM, or SOAR
products. It is designed as an intelligence and orchestration layer
above security telemetry and specialized detection/response components.

## Problem Statement

Modern security environments generate large volumes of alerts from
networks, endpoints, files, devices, applications, and users. These
signals can remain fragmented across tools, creating alert overload,
incomplete incident context, false positives, delayed investigation, and
risk when automation acts on uncertain predictions.

ARGUS addresses this problem by coordinating specialized agents, fusing
evidence, calculating risk, explaining decisions, and using
confidence-aware escalation to decide when automated action is
appropriate and when human review is required.

## Objectives

-   Continuous security-event monitoring.
-   Multi-source threat detection.
-   Specialized agent-based investigation.
-   Cross-agent evidence fusion.
-   Risk scoring from 0--100.
-   Explainable AI-based decisions.
-   MITRE ATT&CK-aware context.
-   Confidence-aware response.
-   Human escalation for uncertain cases.
-   Centralized incident and decision tracking.
-   Feedback-driven improvement.

## Architecture

``` text
Protected Environment
        |
        v
+----------------------+
|     Sentinel AI      |
| Monitoring/Collection|
+----------+-----------+
           |
           v
+-------------------------------+
|       Specialized Agents      |
| Malware | Device | Host | IR  |
|              | Recovery       |
+---------------+---------------+
                |
                v
+----------------------------------------------+
|           ARGUS DEFENSE CORE                 |
| Threat Fusion | Risk Scoring                 |
| Attack Path   | Policy & Decision             |
| XAI           | LLM Security Advisor         |
| Learning Engine                              |
+----------------------+-----------------------+
                       |
                       v
+----------------------------------------------+
|              CONFIDENCE GATE                 |
| Strong/consistent evidence -> controlled     |
| automated response                           |
| Uncertain/conflicting evidence -> human      |
| escalation                                   |
+----------------------+-----------------------+
                       |
                       v
          Response / Recovery / Reporting
```

## Specialized Agents

### Sentinel Agent

The monitoring and intelligence agent. Collects network, process, file,
registry, device, system, web, email, and other authorized security
telemetry.

### Malware Hunter

Analyzes suspicious files and malware indicators using static features,
hashes, behavioral evidence, threat intelligence, and ML models.

### Device Guardian

Monitors external devices such as USB/storage devices and applies
device-security policies.

### Host Protection Agent

Monitors endpoint integrity, processes, registry/startup activity,
persistence, privilege escalation, and ransomware-like behavior.

### Intrusion Response Agent

Handles controlled containment actions such as IP/domain blocking,
endpoint isolation, process termination, firewall updates, and session
containment.

### Recovery Agent

Supports restoration and remediation, including rollback, file recovery,
system-health checks, service recovery, and incident recovery reports.

## ARGUS Defense Core

### Threat Fusion Engine

Correlates evidence from Sentinel, specialized agents, threat
intelligence, and historical context into a unified incident.

### Risk Scoring Engine

Produces an overall 0--100 risk score using threat evidence, severity,
context, confidence, and other validated features.

### Attack Path Prediction

Uses security knowledge and available graph/context information to
reason about possible attacker movement and next steps.

### Policy & Decision Engine

Maps risk and context to permitted actions. Policies can require human
approval for sensitive actions.

### Explainability Engine

Uses XAI such as SHAP to show which model features contributed to a
prediction and to expose supporting or conflicting evidence.

### LLM Security Advisor

Converts structured incident information into analyst-friendly
summaries, explanations, investigation suggestions, and reports. The LLM
is an assistant, not the sole authority for high-impact security
actions.

### Learning Engine

Stores incident outcomes and feedback for later model retraining,
threshold calibration, policy refinement, and system improvement.

## Confidence-Gated Decision Pipeline

The main research direction is confidence-aware response:

``` text
Security Event
     |
     v
Detection + Agent Findings
     |
     v
Threat Fusion
     |
     v
Risk Score
     |
     v
XAI / Evidence Analysis
     |
     v
Confidence Gate
     |
     +----------------------+
     |                      |
 High confidence       Low/conflicting
     |                      |
     v                      v
Controlled action       Human review
     |                      |
     +----------+-----------+
                |
                v
        Report + Feedback
```

A high model probability alone should not automatically authorize an
action. The system should consider evidence strength, consistency, agent
agreement, explainability information, and policy constraints.

Confidence thresholds are a research variable and must be calibrated
experimentally.

## AI/ML Pipeline

### Network Detection

-   CIC-IDS2017 / CSE-CIC-IDS2018
-   Preprocessing and feature selection
-   XGBoost classification
-   Probability estimation
-   SHAP explanation
-   Risk and confidence assessment

### Anomaly Detection

-   Security telemetry
-   Feature extraction
-   Isolation Forest
-   Anomaly score
-   Fusion with other evidence

### Malware Detection

-   EMBER static malware features
-   Feature preprocessing
-   XGBoost or Random Forest
-   Malicious probability
-   Explainability

## Datasets

  Dataset / Source    Primary Purpose
  ------------------- ------------------------------------------
  CIC-IDS2017         Network intrusion detection
  CSE-CIC-IDS2018     Network-security benchmark
  UNSW-NB15           Additional network benchmark
  Edge-IIoTset        IoT/network security research
  EMBER               Static malware-feature classification
  MITRE ATT&CK STIX   Threat knowledge and technique mapping
  VirusTotal API      Optional hash/threat-intelligence lookup

Each dataset should have a defined role. The team should avoid training
every component on every dataset and should use appropriate holdout or
cross-dataset evaluation where possible.

## Technology Stack

### Languages

-   Python 3.10+
-   JavaScript / TypeScript

### Machine Learning

-   pandas
-   NumPy
-   scikit-learn
-   XGBoost
-   PyTorch (future)
-   TensorFlow (optional)

### Explainability

-   SHAP

### LLM / NLP

-   Hugging Face Transformers
-   OpenAI-compatible or other authorized LLM APIs
-   Llama/Mistral-class local models where appropriate

### Cybersecurity

-   Zeek
-   Suricata
-   Sysmon
-   Wazuh / OSSEC
-   YARA
-   MITRE ATT&CK
-   Threat-intelligence APIs

### Backend

-   FastAPI
-   Uvicorn
-   REST
-   WebSockets for live events
-   gRPC as a future option

### Databases

-   SQLite for early prototype
-   PostgreSQL for scalable storage
-   Redis for caching/streams where needed
-   Neo4j for future knowledge-graph capabilities

### Frontend

-   React
-   TypeScript
-   Charting/visualization libraries

### Messaging / Distributed Systems

-   Kafka
-   RabbitMQ
-   Redis Streams

These should be introduced only when the prototype actually requires
distributed messaging.

### DevOps

-   Git
-   GitHub
-   Docker
-   Docker Compose
-   GitHub Actions

### Development and Testing

-   Jupyter
-   pytest
-   Postman / OpenAPI
-   Ruff
-   Black
-   pre-commit

## Prototype Scope

The first working prototype should prioritize an end-to-end path:

``` text
Sentinel
  -> Threat Detection
  -> Threat Fusion
  -> Risk Scoring
  -> SHAP
  -> Confidence Gate
  -> Simulated Response / Human Escalation
  -> Dashboard
```

Recommended first operational agents:

1.  Sentinel
2.  Malware Hunter
3.  Intrusion Response

Device Guardian, Host Protection, and Recovery remain part of the
complete architecture and can be integrated incrementally.

## Repository Structure

``` text
argus-defense-core/
├── README.md
├── LICENSE
├── .gitignore
├── .env.example
├── docker-compose.yml
├── requirements.txt
├── pyproject.toml
├── docs/
│   ├── architecture/
│   ├── research/
│   ├── api/
│   └── diagrams/
├── data/
│   ├── raw/
│   ├── processed/
│   └── README.md
├── models/
│   ├── xgboost/
│   ├── anomaly/
│   └── artifacts/
├── backend/
│   ├── app/
│   │   ├── main.py
│   │   ├── api/
│   │   ├── core/
│   │   ├── database/
│   │   ├── schemas/
│   │   └── services/
│   └── tests/
├── agents/
│   ├── sentinel/
│   ├── malware_hunter/
│   ├── device_guardian/
│   ├── host_protection/
│   ├── intrusion_response/
│   └── recovery/
├── ml/
│   ├── preprocessing/
│   ├── training/
│   ├── evaluation/
│   ├── explainability/
│   └── confidence_gate/
├── knowledge/
│   ├── mitre/
│   ├── threat_intelligence/
│   └── graph/
├── frontend/
│   └── argus-dashboard/
├── scripts/
└── tests/
    ├── unit/
    ├── integration/
    └── evaluation/
```

## Evaluation

### ML Metrics

-   Accuracy
-   Precision
-   Recall
-   F1-score
-   ROC-AUC
-   PR-AUC where appropriate
-   Confusion matrix

### Security Metrics

-   False-positive rate
-   False-negative rate
-   Detection rate
-   Threat classification performance

### System Metrics

-   Detection latency
-   Decision latency
-   Response latency
-   API latency
-   CPU/RAM usage
-   Event throughput

### Confidence-Gate Metrics

-   Percentage automatically handled
-   Percentage escalated
-   Accuracy of auto-action cases
-   Error rate among auto-action cases
-   Confidence calibration
-   Threshold sensitivity
-   Human-review workload

The objective is not to maximize automation. The objective is to find a
useful and safe operating point.

## Research Direction

The current research direction combines:

``` text
Model Probability
        +
Evidence Strength
        +
Evidence Consistency
        +
Agent Agreement
        +
XAI Information
        |
        v
Confidence / Trust Assessment
        |
        v
Autonomous Action OR Human Escalation
```

ARGUS should not claim worldwide uniqueness merely because it combines
AI, agents, XAI, or an LLM. Novelty must be established through a
current literature review, clear technical contribution, and
reproducible experiments.

## Development Roadmap

### Phase 1 --- Foundation

-   Repository and environment
-   Dataset pipeline
-   Sentinel ingestion
-   Event schema
-   FastAPI skeleton
-   Dashboard skeleton

### Phase 2 --- Core Intelligence

-   XGBoost
-   Isolation Forest
-   Threat fusion
-   Risk scoring
-   SHAP

### Phase 3 --- Confidence Mechanism

-   Confidence calculation
-   Threshold calibration
-   Agent conflict handling
-   Human escalation workflow

### Phase 4 --- Agent Integration

-   Malware Hunter
-   Intrusion Response
-   MITRE ATT&CK
-   LLM Security Advisor

### Phase 5 --- Evaluation

-   Benchmark testing
-   Cross-dataset testing where feasible
-   Latency testing
-   Confidence calibration
-   Failure-case analysis

### Phase 6 --- Expansion

-   Device Guardian
-   Host Protection
-   Recovery Agent
-   Neo4j knowledge graph
-   Distributed messaging
-   Advanced attack-path reasoning
-   Continuous learning

## Team Responsibilities

  -----------------------------------------------------------------------
  Role                                Primary Responsibility
  ----------------------------------- -----------------------------------
  Frontend                            React dashboard, visualization,
                                      incident investigation UI

  Backend                             FastAPI, orchestration, APIs,
                                      database, agent integration

  AIML 1                              XGBoost, threat classification,
                                      risk model, evaluation

  AIML 2                              Isolation Forest, SHAP, confidence
                                      gate, calibration

  Data Engineer                       Dataset preparation, ETL, feature
                                      pipelines, MITRE data
  -----------------------------------------------------------------------

## Project Status

**Status: Research Prototype / Active Development**

### Core prototype

-   [ ] Sentinel ingestion
-   [ ] Network threat model
-   [ ] Anomaly detection
-   [ ] Threat fusion
-   [ ] Risk scoring
-   [ ] SHAP explanation
-   [ ] Confidence Gate
-   [ ] Malware Hunter
-   [ ] Intrusion Response
-   [ ] MITRE ATT&CK integration
-   [ ] LLM Security Advisor
-   [ ] React dashboard
-   [ ] API integration
-   [ ] Evaluation pipeline

### Planned expansion

-   [ ] Device Guardian
-   [ ] Host Protection
-   [ ] Recovery Agent
-   [ ] Neo4j knowledge graph
-   [ ] Distributed messaging
-   [ ] Advanced attack-path prediction
-   [ ] Continuous learning

## Future Work

Potential research directions include:

-   Graph Neural Networks for attack-path reasoning.
-   Digital Twin-based cyber-defense simulation.
-   Federated Learning.
-   Adaptive security agents.
-   Multi-agent conflict resolution.
-   Calibrated uncertainty estimation.
-   Cost- and latency-aware agent orchestration.
-   Autonomous security playbooks.
-   Continual learning.
-   Large-scale threat-intelligence knowledge graphs.
-   Controlled LLM tool use for security workflows.
-   Cross-environment model generalization.
-   Production-scale distributed deployment.

## Security and Safety

ARGUS is intended for authorized defensive security research.

Principles:

-   Least privilege.
-   Secure authentication.
-   Role-based access control.
-   Audit logging.
-   Encrypted communication.
-   Secure secret management.
-   Human approval for high-impact actions when required.
-   Sandboxed testing.
-   No unauthorized scanning or exploitation.
-   Controlled response actions in demonstrations.
-   Clear separation between detection and execution privileges.

Destructive response actions should be simulated unless the team is
operating inside an isolated and explicitly authorized test environment.

## License

The project team should select an appropriate open-source license after
reviewing the licensing requirements of the project code, datasets,
third-party libraries, APIs, and research material.

Potential software licenses to evaluate include:

-   MIT License
-   Apache License 2.0

Third-party datasets and tools may have separate licenses and must be
reviewed independently.

------------------------------------------------------------------------

## ARGUS Defense Core

**Detect → Investigate → Fuse → Assess → Explain → Trust → Respond →
Learn**

> **ARGUS doesn't just detect threats --- it evaluates when it should
> trust its own decision.**
