# 🚀 Exam Day 0-Minute Setup Protocol

Follow these exact steps the moment your exam begins to stand up your boilerplate repository. Do not use Qoder for these steps; execute them manually in the terminal.

## Phase 1: Preparation
1. Download or transfer `boilerplate_repo.zip` to your lab machine.
2. Extract the ZIP file into your workspace directory (e.g., `Desktop/COMS3011A_Exam`).
3. Open your IDE (Qoder/VSCode) and open the extracted root folder.
4. Open a new Terminal inside your IDE.

---

## Phase 2: Backend Setup (Python)
In your first terminal tab, run the following commands line by line:

```bash
cd backend
python -m venv venv

# ACTIVATE THE VIRTUAL ENVIRONMENT
# If on Windows (likely for lab machines):
.\venv\Scripts\activate
# If on Linux/Mac:
source venv/bin/activate

# INSTALL DEPENDENCIES
pip install fastapi "uvicorn[standard]" sqlmodel pydantic

# START THE BACKEND SERVER
uvicorn main:app --reload --port 8000
```
*Leave this terminal tab open and running.*

---

## Phase 3: Frontend Setup (React/Node)
Open a **second** terminal tab in your IDE (ensure you are back at the root folder), and run:

```bash
cd frontend

# INITIALIZE VITE (The --force flag keeps your pre-written App.tsx)
npm create vite@latest . -- --template react-ts --force

# INSTALL DEPENDENCIES
npm install
npm install -D tailwindcss postcss autoprefixer

# INITIALIZE TAILWIND
npx tailwindcss init -p

# START THE FRONTEND SERVER
npm run dev
```
*Leave this terminal tab open and running.*

---

## Phase 4: Verification & Agent Lock-in
1. **Verify Connection:** Open your browser and navigate to `http://localhost:5173`. You should see your dashboard and the text: **"Backend Status: Backend API is running"**.
2. **Lock in Qoder:** Open Qoder's chat interface. Ensure `AGENTS.md` is visible or pinned to the context.
3. **First Prompt:** Type the following to initialize the agent: 
   > *"Read `AGENTS.md`. Acknowledge that you are in Builder/Architect mode and will strictly follow the STE and token efficiency rules. Do not write any code yet."*

You are now fully set up, connected, and ready to start reading the exam brief. Good luck!