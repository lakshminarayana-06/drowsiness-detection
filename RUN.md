# How to Run the Whole Project (WakeGuard)

Everything you need to run the app successfully. No database — uses local JSON storage.

---

## 1. Prerequisites

Install these once:

| What | Version | Check |
|------|---------|--------|
| **Node.js** | 18+ | `node -v` |
| **npm** | comes with Node | `npm -v` |
| **Python** | 3.10+ | `python --version` or `py -3 --version` |

---

## 2. One-time setup

Open a terminal in the project root (`Content-Analyser`).

### Backend (Python)

```bash
pip install -r server/requirements.txt
```

This installs: **fastapi**, **uvicorn**, **pydantic**. Nothing else (no database drivers).

### Frontend (Node)

```bash
npm install
```

This installs React, Vite, and all client dependencies.

---

## 3. Run the whole project (development)

You need **two terminals** in the project root.

### Terminal 1 — Backend (port 5000)

```bash
npm run dev:server
```

Or:

```bash
uvicorn server.main:app --reload --host 0.0.0.0 --port 5000
```

Leave this running. You should see something like: `Uvicorn running on http://0.0.0.0:5000`.

### Terminal 2 — Frontend (port 5173)

```bash
npm run dev:client
```

Or:

```bash
npx vite
```

Leave this running. Vite will show: `Local: http://localhost:5173/`.

### Use the app

- Open a browser at: **http://localhost:5173**
- The frontend will call the API at `/api/...`; Vite proxies those requests to the Python backend on port 5000.

---

## 4. Run for production (single server)

Build the frontend and serve it from the Python server:

```bash
npm run build
npm run start:py
```

Then open **http://localhost:5000**. The same process serves both the API and the React app.

---

## 5. What the backend provides (no extra setup)

- **Storage**: Data is saved in `server/data/store.json` (created automatically). No database or env vars.
- **API**:
  - `POST /api/sessions` — start a monitoring session
  - `PATCH /api/sessions/:id/end` — end a session with stats
  - `POST /api/events` — log a drowsiness event
  - `GET /api/stats` — total sessions, alerts, average duration
- **Seed**: On first start, one sample session is added so the Results page has data.

---

## 6. Quick checklist

- [ ] Node and npm installed → `npm install` done
- [ ] Python 3.10+ installed → `pip install -r server/requirements.txt` done
- [ ] Terminal 1: backend running on port 5000
- [ ] Terminal 2: frontend running on port 5173
- [ ] Browser: http://localhost:5173

---

## 7. Troubleshooting

| Problem | Fix |
|--------|-----|
| **"Module not found" (Python)** | Run `pip install -r server/requirements.txt` from project root. |
| **"Cannot GET /api/sessions" or 404** | Start the backend first (Terminal 1). Ensure it’s on port 5000. |
| **Blank page or API errors in browser** | Open http://localhost:5173 (not 5000) in dev. In dev, the app is served by Vite; only API calls go to 5000. |
| **Port 5000 already in use** | Stop the other app using 5000, or run backend on another port: `uvicorn server.main:app --reload --port 5001` and in `vite.config.ts` set proxy target to `http://localhost:5001`. |
| **Data gone after restart** | Data lives in `server/data/store.json`. If the file is missing or the folder was deleted, the store is recreated empty (plus seed). |

---

## 8. Project layout (what runs)

```
Content-Analyser/
├── client/          ← React app (Vite)
├── server/
│   ├── main.py      ← FastAPI app (entry)
│   ├── routes.py    ← /api/sessions, /api/events, /api/stats
│   ├── local_storage.py  ← JSON file storage
│   ├── schemas.py   ← request/response models
│   ├── storage.py   ← re-exports local_storage
│   └── data/        ← store.json (created at first run)
├── shared/          ← API paths/types (used by frontend)
├── package.json     ← npm scripts
└── RUN.md           ← this file
```

You have everything you need: backend (Python + local storage) and frontend (React + Vite). No database or extra services.
