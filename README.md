# Adaptive-Explainable-Network-Intrusion-Detection-Security-Log-Anomaly-Correlation
# AI-NIDS LAC


AI-NIDS SOC V2 is a defensive cybersecurity platform designed to analyze
network telemetry and security logs, detect anomalous behavior, classify
potential threats, correlate security events, and present actionable
security insights through a centralized SOC dashboard.

The platform combines machine learning, behavioral analysis, anomaly
detection, threat classification, explainable AI, risk scoring, event
correlation, and real-time monitoring into a unified security monitoring
environment.

---

## Overview

Traditional intrusion detection systems often rely heavily on predefined
signatures and static rules. AI-NIDS SOC V2 extends this approach by
combining machine-learning-based anomaly detection with behavioral
correlation and contextual security analysis.

The platform processes security telemetry through a multi-stage pipeline:

    Telemetry Ingestion
            ↓
    Schema Detection
            ↓
    Canonical Data Normalization
            ↓
    Feature Engineering
            ↓
    Anomaly Detection
            ↓
    Threat Classification
            ↓
    Behavioral Correlation
            ↓
    Risk Scoring
            ↓
    Explainable AI (XAI)
            ↓
    Incident Analysis
            ↓
    SOC Dashboard

This architecture allows the platform to analyze both individual security
events and broader behavioral patterns.

---

## Key Features

### 1. Security Telemetry Ingestion

AI-NIDS SOC V2 supports structured security data ingestion from common
formats including:

- CSV
- JSON
- JSON Lines
- Excel/XLSX
- Structured TXT/LOG data
- Security-log datasets
- Network-flow datasets

The ingestion layer performs schema identification and normalization before
the data enters the detection pipeline.

---

### 2. Security Log Analysis

The platform analyzes structured security logs using features such as:

- Event ID
- Event level
- Component
- Event template
- Message patterns
- Event frequency
- Temporal behavior
- Severity indicators
- Authentication-related activity
- Off-hours activity

This allows the system to identify unusual log behavior without treating
every unusual record as a confirmed attack.

---

### 3. Network Flow Analysis

Network telemetry can be analyzed using characteristics such as:

- Source IP
- Destination IP
- Source port
- Destination port
- Protocol
- Packet volume
- Byte volume
- Connection frequency
- Connection states
- Temporal traffic patterns

These features support behavioral detection of suspicious network activity.

---

## AI Detection Engine

The detection architecture combines machine learning with behavioral
security analysis.

### Isolation Forest

Isolation Forest is used for unsupervised anomaly detection.

It identifies observations that differ significantly from learned behavioral
patterns.

Typical applications include:

- Unusual network activity
- Abnormal event frequency
- Unexpected security-log behavior
- Traffic bursts
- Unusual connection patterns

---

### Random Forest Classification

A Random Forest classifier is used for supervised threat classification.

Supported threat categories include:

- NORMAL
- DDOS
- PORT_SCAN
- BRUTE_FORCE
- BOTNET
- SUSPICIOUS_ACTIVITY

Ground-truth labels, when available in datasets, are treated as evaluation
information rather than being used directly as inference features.

---

## Behavioral Threat Detection

AI-NIDS SOC V2 combines machine-learning predictions with behavioral
correlation.

### DDoS Detection

DDoS-like behavior can be identified using evidence such as:

- High traffic rates
- High packet rates
- High byte rates
- Abnormally high connection frequency
- Multiple sources targeting a destination
- Concentrated traffic patterns

---

### Port Scan Detection

Port-scanning behavior can be identified using patterns such as:

- One source contacting many destination ports
- One source contacting multiple hosts
- High unique destination-port counts
- Repeated failed connections
- Short-window probing behavior

---

### Brute Force Detection

Brute-force behavior can be identified through:

- Repeated authentication failures
- Repeated attempts from the same source
- Multiple account attempts
- High authentication-failure frequency
- Failure patterns concentrated within a time window

Behavioral detection is based on observable telemetry rather than filenames
or dataset names.

---

## Explainable AI

AI-NIDS SOC V2 provides contextual explanations for security detections.

Instead of displaying only:

    Threat detected

the platform provides supporting information based on observed features,
behavioral patterns, anomaly scores, and event context.

Example:

    Repeated authentication failures were detected from the same source
    within a short observation window.

This allows security analysts to understand why an event was considered
suspicious.

---

## Risk Scoring

Each analyzed event can receive a dynamic risk score based on available
security evidence.

Risk assessment can incorporate factors such as:

- Anomaly score
- Threat classification
- Behavioral evidence
- Severity
- Correlation evidence
- Event characteristics

Risk levels are presented through the SOC dashboard to help prioritize
security events.

---

## Event Correlation

The correlation engine groups related security events into behavioral
patterns and potential incidents.

For example:

    Multiple authentication failures
             +
    Same source
             +
    Short time window
             ↓
    Potential Brute Force Incident

This helps distinguish individual events from larger security incidents.

---

## Operating Modes

AI-NIDS SOC V2 supports multiple monitoring modes.

### DEMO MODE

Uses controlled synthetic security events for demonstration and UI testing.

### DATASET MODE

Analyzes uploaded security datasets and maintains dataset-specific analysis
results.

### LIVE MODE

Designed for authorized real-time telemetry sources and security monitoring.

The dashboard displays the active operating mode to distinguish synthetic,
dataset-based, and live telemetry.

---

## Dataset Isolation

Each uploaded dataset is associated with its own dataset/session context.

This allows the platform to distinguish:

- Current Dataset
- Previous Datasets
- Historical SOC Data
- Demo Data

Dataset-specific statistics can therefore be analyzed independently from
historical security activity.

---

## SOC Dashboard

The platform provides a centralized SOC interface containing sections
for:

- Overview
- Live Monitor
- Network Flows
- Security Logs
- Threats
- Incidents
- AI Analysis & XAI
- Datasets
- Reports
- Settings & Audit

### Overview

The Overview dashboard provides high-level visibility into:

- Total Events
- Anomalies
- Critical Alerts
- Network Flows
- Security Logs
- Threat Distribution
- Recent Security Events
- Detection Pipeline

---

## Technology Stack

### Backend

- Python
- FastAPI
- Uvicorn
- SQLite
- Pandas
- Scikit-learn
- PyJWT
- OpenPyXL

### Machine Learning

- Scikit-learn
- Isolation Forest
- Random Forest
- Feature Engineering
- Behavioral Analysis

### Communication

- REST APIs
- WebSockets

### Frontend

- HTML
- CSS
- JavaScript
- SOC dashboard interface

---

## Project Structure

```text
AI-NIDS-V2-fixed/
│
├── backend/
│   │
│   ├── app/
│   │   ├── main.py
│   │   ├── auth.py
│   │   ├── database.py
│   │   ├── ingest.py
│   │   └── schemas.py
│   │
│   ├── ai/
│   │   ├── feature_engineering.py
│   │   ├── anomaly_detector.py
│   │   ├── risk_engine.py
│   │   ├── explainability.py
│   │   └── behavior_engine.py
│   │
│   ├── ml/
│   ├── network/
│   ├── data/
│   ├── nids.db
│   ├── requirements.txt
│   ├── sample_logs.csv
│   └── seed_demo.py
│
├── backend_v1_backup/
│
├── tests/
│   ├── test_ai.py
│   ├── test_api.py
│   ├── test_correlation.py
│   ├── test_ingest.py
│   └── test_v2_validation.py
│
└── README.md
