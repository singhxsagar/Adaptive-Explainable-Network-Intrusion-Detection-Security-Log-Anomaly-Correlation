# AI-NIDS SOC Platform V2

Adaptive Network Intrusion Detection & Security Log Anomaly Correlation Platform powered by FastAPI, SQLite, Dual-Ensemble ML, Explainable AI (XAI), and Real-Time WebSockets.

---

## Overview
AI-NIDS SOC V2 is a defensive cybersecurity monitoring platform designed to analyze network flow telemetry and security log events. It combines unsupervised anomaly detection (Isolation Forest) with supervised threat classification (Random Forest), behavioral baselining, explainable risk scoring, and multi-stage event correlation.

---

## Key Features
1. **Multi-Mode Support**:
   - **`DEMO` Mode**: Safe demonstration using synthetic generated security events.
   - **`DATASET` Mode**: Ingest and analyze uploaded `.csv`, `.json`, `.xlsx`, `.txt`, and `.log` security logs. Schema validation rejects unrelated files before AI analysis.
   - **`LIVE` Mode**: Monitor authorized local Windows Security Event Log telemetry (or supported local auth logs) with truthful sensor status and real-time WebSocket delivery.
2. **Flexible Schema Normalization**: Automatic alias mapping (`source_ip`, `src_ip`, `Source IP` -> `src_ip`) for Network Flow and Security Log data.
3. **Excel (.xlsx) Multi-Sheet Support**: Sheet inspection and worksheet selector for multi-sheet workbooks.
4. **Dual Ensemble AI Architecture**:
   - **Isolation Forest**: Detects unknown, novel anomalies.
   - **Random Forest**: Classifies known threat categories (`DDoS-like`, `Port-scan-like`, `Brute-force-like`, `Botnet-like`, `Suspicious Activity`).
5. **Unknown Anomaly Distinction**: Clearly distinguishes `UNKNOWN ANOMALY` from known threat classifications.
6. **Explainable AI (XAI)**: Provides human-readable feature contribution breakdowns ("WHY WAS THIS FLAGGED?").
7. **Multi-Stage Event Correlation Engine**: Correlates multi-stage security events into high-level incidents with visual timelines.
8. **Dynamic Risk Engine**: Computes 0–100 risk scores with configurable severity thresholds (`LOW`, `MEDIUM`, `HIGH`, `CRITICAL`).
9. **Real-time WebSockets**: Live event streaming to modern dark SOC dashboard UI.
10. **Authentication & RBAC**: Role-Based Access Control (`ADMIN`, `ANALYST`, `VIEWER`) and Audit Logging.
11. **Report Generation**: Export SOC reports in CSV and HTML formats.
12. **Docker Ready**: Production container configuration with `Dockerfile` and `docker-compose.yml`.

---

## Project Structure
```
AI-NIDS/
├── backend/
│   ├── ai/
│   │   ├── anomaly_detector.py      # Isolation Forest anomaly detector
│   │   ├── classifier.py            # Random Forest threat classifier
│   │   ├── feature_engineering.py   # Network/Log feature extractor
│   │   ├── model_manager.py         # Model persistence & metadata
│   │   ├── baseline.py              # Behavioral baseline analyzer
│   │   ├── explainability.py        # Explainable AI (XAI) engine
│   │   ├── correlation_engine.py    # Multi-stage event correlation engine
│   │   └── risk_engine.py           # Dynamic risk scoring engine
│   ├── app/
│   │   ├── main.py                  # FastAPI application & SOC Dashboard SPA
│   │   ├── database.py              # SQLite database & migrations
│   │   ├── detector_engine.py       # Detection pipeline wrapper
│   │   ├── ingest.py                # CSV/JSON/XLSX ingestion & normalizer
│   │   ├── schemas.py               # Canonical schemas & ALIAS_MAP
│   │   ├── auth.py                  # JWT authentication & RBAC
│   │   ├── audit.py                 # Audit trail logger
│   │   ├── reports.py               # CSV/HTML report generator
│   │   └── websocket_manager.py     # Real-time WebSocket manager
│   ├── network/
│   │   ├── collector.py             # Authorized local telemetry collector
│   │   └── sensor_manager.py        # Truthful sensor state manager
│   ├── nids.db                      # SQLite database
│   ├── seed_demo.py                 # Safe demo database seeder
│   └── requirements.txt             # Python dependencies
├── sample_datasets/                 # Downloadable sample datasets (.csv, .xlsx)
├── tests/                           # Pytest automated test suite
├── docs/                            # Comprehensive documentation suite
├── models/                          # Persisted model joblib files & metadata
├── Dockerfile                       # Container definition
├── docker-compose.yml               # Docker Compose file
└── README.md                        # Documentation
```

---

## Quick Start (Windows Setup)

### Prerequisites
- Python 3.11+ (Python 3.13 recommended)

### 1. Installation & Environment Setup
Open PowerShell in the project directory:
```powershell
python -m venv .venv
.venv\Scripts\Activate.ps1
pip install -r backend/requirements.txt openpyxl pyjwt pytest websockets httpx
```

### 2. Seed Safe Demo Data
```powershell
python backend/seed_demo.py
```

### 3. Launch Development Server
```powershell
uvicorn backend.app.main:app --reload --host 127.0.0.1 --port 8000
```
Open your browser at **`http://127.0.0.1:8000`**.

---

## Running with Docker
```bash
docker-compose up -d --build
```
Access the application at `http://localhost:8000`.

---

## Running Tests
Execute the pytest automated test suite:
```powershell
python -m pytest
```

---

## Operating Modes

### DEMO MODE
Generates synthetic, safe lab demonstration events to showcase SOC dashboard capabilities without accessing real networks.

### DATASET MODE
Upload `.csv`, `.json`, or `.xlsx` security files. Click **Ingest Dataset** in the dashboard or use `/api/ingest`. If uploading an Excel file with multiple sheets, you can select the target worksheet.

### LIVE MODE
Monitors authorized local system telemetry. The sensor status explicitly displays `LIVE SENSOR: CONNECTED` or `NOT CONFIGURED`. No fake live traffic is generated.

---

## Security & Ethical Considerations
- **Strictly Defensive**: This application contains **no offensive attack functionality**, exploit execution, scanning tools, or credential theft logic.
- **Authorized Scope**: Live telemetry monitoring must only be run on networks and systems you are explicitly authorized to monitor.
- **File Upload Security**: Uploaded files are treated strictly as data, validated for mime/extension, and saved outside executable paths.

---

## Documentation
See the `docs/` folder for detailed guides:
- `docs/architecture.md`: System topology & module structure
- `docs/ai-pipeline.md`: AI detection & correlation pipeline
- `docs/dataset-format.md`: Supported column schemas & aliases
- `docs/api.md`: Complete REST & WebSocket API specification
- `docs/deployment.md`: Detailed deployment procedures
- `docs/research.md`: Defensive methodology & research objectives
