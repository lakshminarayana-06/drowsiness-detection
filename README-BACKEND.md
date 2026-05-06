# WakeGuard Backend (Python)

Uses **local JSON file storage** — no database required. Ideal for college projects.

Data is stored in `server/data/store.json` and persists across server restarts.

## Setup

1. **Create a virtual environment** (recommended):

   ```bash
   cd Content-Analyser
   python -m venv .venv
   .venv\Scripts\activate   # Windows
   # source .venv/bin/activate   # macOS/Linux
   ```

2. **Install dependencies**:

   ```bash
   pip install -r server/requirements.txt
   ```

No database or environment variables needed.

## Run

From the **project root** (`Content-Analyser`):

```bash
uvicorn server.main:app --reload --host 0.0.0.0 --port 5000
```

Or: `npm run dev:server`

- **Development**: Start the backend on port 5000, then in another terminal run `npm run dev:client`. Vite proxies `/api` to the backend.
- **Production**: Run `npm run build`, then start the Python server; it serves the API and the static frontend.

## API

| Method | Path | Description |
|--------|------|-------------|
| POST   | `/api/sessions`         | Create session |
| PATCH  | `/api/sessions/:id/end` | End session |
| POST   | `/api/events`           | Log drowsiness event |
| GET    | `/api/stats`            | Aggregate stats |

Responses use **camelCase** to match the frontend.
