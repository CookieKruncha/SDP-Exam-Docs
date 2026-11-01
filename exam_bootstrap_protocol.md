# 0-Minute Exam Bootstrap Protocol

If pre-built code is not allowed, follow these two phases immediately at 08:30 AM when coding begins.

## PHASE 1: Human Terminal Execution (Do Not Use Agent)
*Why: Doing this yourself takes 45 seconds, uses 0 tokens, and guarantees no environment hallucinations.*

Open your terminal and paste this exact block:

```bash
mkdir sdp_exam && cd sdp_exam
git init
mkdir backend && cd backend
python -m venv venv
source venv/bin/activate # (Use venv\Scripts\activate on Windows)
pip install fastapi uvicorn sqlalchemy pydantic sqlite3
echo "fastapi\nuvicorn\nsqlalchemy\npydantic\nsqlite3" > requirements.txt
cd ..
npm create vite@latest frontend -- --template react-ts
cd frontend
npm install
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p
npm install lucide-react recharts @tanstack/react-table
cd ..
```

## PHASE 2: Agent Code Generation
*Why: Now that the environment exists, feed Qoder this exact prompt to populate the core files.*

**COPY-PASTE THIS PROMPT TO QODER:**

> Builder Mode. 
> The project has a `/backend` (FastAPI) and `/frontend` (React+Vite) folder. Dependencies are installed.
> Generate the following 4 boilerplate files to connect the stack. Do not explain the code.
> 
> 1. `backend/database.py`: Setup a basic SQLite SQLAlchemy engine (local file `app.db`) and a `get_db` dependency.
> 2. `backend/main.py`: Setup FastAPI app, add CORS middleware allowing `http://localhost:5173`, and include a simple `/health` GET route.
> 3. `frontend/tailwind.config.js`: Configure Tailwind to scan `./index.html` and `./src/**/*.{js,ts,jsx,tsx}`.
> 4. `frontend/src/App.tsx`: Create a basic full-screen layout with a top navigation bar and a main content area using Tailwind CSS. Include a state that fetches from `/health` on mount and displays the status.