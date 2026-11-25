# Scam Shield+ Backend (FastAPI)

Modular Python FastAPI backend for **Scam Shield+** — AI voice deepfake screening, coercion phrase detection, non-blocking `ntfy.sh` family alerts, DetectifAI feedback reporting, and 1-page cybercrime evidence PDF generation.

## Endpoints

- `GET /health` — Health & environment readiness check.
- `POST /api/analyze` — Multipart form upload (`file`, optional `family_member_name`, optional `transcript`). Validates non-empty audio (>4s to 300s), computes SHA-256, calls DetectifAI `/v1/deepfake/detect`, checks coercion indicators, triggers non-blocking `ntfy.sh` alert on `high` risk, and returns risk + callback guidance.
- `POST /api/feedback` — JSON payload (`operation_id`, `verdict`, optional `correct`, `original_verdict`, `note`) forwarded to DetectifAI `/v1/operations/{operation_id}/feedback`.
- `POST /api/evidence-pdf` — Generates a downloadable 1-page PDF report with timestamp, SHA-256 hash, DetectifAI verdict/score, disclaimer, and Indian Cybercrime Helpline (`1930` / `cybercrime.gov.in`) guidance.

## Run on Windows Command Prompt (`cmd.exe`)

```bat
cd /d d:\projects\scam-shield\backend
python -m venv .venv
.venv\Scripts\activate
pip install -r requirements.txt
copy .env.example .env
notepad .env
uvicorn app.main:app --reload --host 0.0.0.0 --port 8000
```

Interactive Swagger docs will be available at `http://localhost:8000/docs`.
