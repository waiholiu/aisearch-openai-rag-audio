# VS Code Debug Configuration

## Quick Start

Press **F5** to run the application locally with debugging enabled.

## Available Debug Configurations

### 1. **Python: Backend (F5)** - Default
- Builds the frontend (production build)
- Starts the Python backend with debugger
- Backend serves the built frontend from `app/backend/static/`
- Access at: http://localhost:8765

**Best for**: Testing with production-like frontend build

### 2. **Python: Backend Only (no frontend build)**
- Starts only the Python backend with debugger
- No frontend build step (faster startup)
- Uses existing built frontend in `app/backend/static/`

**Best for**: Backend-only changes when frontend is already built

### 3. **Full Stack (Backend + Frontend Dev Server)** - Compound
- Starts Python backend with debugger
- Starts Vite dev server for frontend with hot-reload
- Frontend at: http://127.0.0.1:5173 (with live reload)
- Backend at: http://localhost:8765

**Best for**: Frontend development with hot-reload

## Prerequisites

Before running, ensure:
1. ✅ `.env` file exists in `app/backend/.env` (created by `azd up`)
2. ✅ Python virtual environment exists (`.venv/`)
3. ✅ Frontend dependencies installed (`npm install` in `app/frontend/`)
4. ✅ Deployed to Azure at least once (`azd up`) to have valid Azure resources

## Environment Variables

The backend requires these environment variables (from `app/backend/.env`):
- `AZURE_OPENAI_ENDPOINT`
- `AZURE_OPENAI_REALTIME_DEPLOYMENT`
- `AZURE_SEARCH_ENDPOINT`
- `AZURE_SEARCH_INDEX`
- `AZURE_TENANT_ID`

## Debugging Tips

### Setting Breakpoints
- Set breakpoints in Python files (e.g., `app/backend/app.py`, `ragtools.py`, `rtmt.py`)
- Press F5 to start debugging
- Breakpoints will pause execution

### Key Files to Debug
- `app/backend/app.py` - Main application entry point
- `app/backend/rtmt.py` - WebSocket proxy and tool execution
- `app/backend/ragtools.py` - Search and grounding tools

### Viewing Logs
- Console output appears in the integrated terminal
- Look for messages prefixed with logger names: `voicerag`

## Troubleshooting

### "Module not found" errors
```bash
# Reinstall Python dependencies
source .venv/bin/activate
pip install -r app/backend/requirements.txt
```

### Frontend not loading
```bash
# Rebuild frontend
cd app/frontend
npm run build
```

### Authentication errors
```bash
# Re-authenticate with Azure
azd auth login
```

### Port already in use
- Check if another instance is running on port 8765
- Kill the process: `lsof -ti:8765 | xargs kill -9`
