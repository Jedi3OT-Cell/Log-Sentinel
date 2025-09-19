# Log Sentinel – Security Log Dashboard

Parse SSH/HTTP logs into SQLite, detect brute-force and scan patterns, and visualize activity in Streamlit.

## Quickstart
```bash
python -m venv .venv && source .venv/bin/activate     # Windows: .venv\Scripts\Activate.ps1
pip install -r requirements.txt

# 1) Ingest sample logs → creates data/logs.db
python scripts/parse_logs.py --type apache --input data/sample_apache.log --db data/logs.db
python scripts/parse_logs.py --type ssh    --input data/sample_auth.log   --db data/logs.db --year 2024 --tz -0400

# 2) Detect alerts
python scripts/analyze_logs.py --db data/logs.db --ssh-threshold 5 --ssh-window-min 10 --http404-threshold 3 --http-window-min 5

# 3) Run dashboard
streamlit run app.py
