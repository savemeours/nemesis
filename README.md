# Nemesis
Nemesis is the public-facing investigative interface as the result of Operation Diponegoro, initiated by Abil Sudarman School of Artificial Intelligence. We ingest millions of rows of procurement data, surface anomalies, and make the findings legible to citizens, journalists, and policymakers.

https://assai.id/nemesis


> End the vampire ball.


## Release Status

| Asset | Status | ETA |
|-------|--------|-----|
| Dashboard URL | 🟡 In progress | 17 April |
| Fine-tuned model | 🟡 In progress | ? |


Stay tuned.

## Downloads

### Dataset

[Download SIRUP raw jsonl dataset (analyzed by GPT-5.4)](https://contenflowstorage.blob.core.windows.net/shared/gpt-5.4-analyzed-sirup.zip?sp=r&st=2026-04-16T12:00:08Z&se=2029-04-16T20:15:08Z&spr=https&sv=2025-11-05&sr=b&sig=m%2FATynnnZq5gSdP8xWWw2ew41EMJZz09fDQRwpbWolk%3D)

[Download SIRUP dataset SQL Ver (analyzed by GPT-5.4-mini)](https://contenflowstorage.blob.core.windows.net/shared/datasets/dashboard.sql?sp=r&st=2026-04-16T12:16:15Z&se=2029-04-16T20:31:15Z&spr=https&sv=2025-11-05&sr=b&sig=sKPH9uazyLcYcSwhARcEwVSG%2FTld9VnGJgZ2mOZIxrA%3D)


### Model
Stay tuned

## Run locally

### 1. Install backend dependencies

Use Node.js 22 or 24 and npm.

```bash
cd backend
npm ci
```

### 2. Import the dashboard database

Download the SQL dataset linked above. If it is archived, extract it first. From the `backend` directory, import the SQL dump into the SQLite database used by the application.

```bash
npm run db:import -- --in /path/to/dashboard.sql
```

Replace `/path/to/dashboard.sql` with the path to your downloaded file. The command writes to `backend/data/dashboard.sqlite` by default. It also accepts SQLite backups with a `.sqlite`, `.sqlite3`, or `.db` extension. If you already have a dashboard database in use, stop the backend and back it up before importing.

### 3. Start the application

**1. Start the backend** from the `backend` directory.

```bash
npm start
```

The backend uses port 3000 by default. Open `http://127.0.0.1:3000/api/health` to confirm it is responding.

**2. Serve the frontend** from the repository root in a second terminal.

```bash
cd frontend
python3 -m http.server 8080
```

Then open `http://127.0.0.1:8080` in your browser.

The frontend is preconfigured to call the backend at `http://127.0.0.1:3000/api`.

## Notes

- No frontend build step required — plain HTML/CSS/JS.
- For development mode with hot reload:
```bash
  cd backend
  npm run dev
```

## Environment

Backend config is loaded from `backend/.env`. Default values:

```env
PORT=3000
CORS_ORIGIN=*
SQLITE_PATH=data/dashboard.sqlite
AUDIT_DATASET_DIR=dataset
GEO_ROOT_PATH=seed/geo
```
