> AGENT INSTRUCTION: When asked to create backend routes or data models, follow these exact patterns. Do not invent new structures.

# 1. Pydantic Data Models (Strict Types)
Always define the shape of the data before writing the logic.

```python
from pydantic import BaseModel
from typing import List, Optional
from datetime import datetime

class CommitMetric(BaseModel):
    hash: str
    author: str
    lines_added: int
    lines_removed: int
    timestamp: datetime

class MetricResponse(BaseModel):
    success: bool
    data: Optional[List[CommitMetric]] = None
    error: Optional[str] = None
```

# 2. FastAPI Router & Endpoint Boilerplate
Always use Dependency Injection for the database and return structured responses.

```python
from fastapi import APIRouter, Depends, HTTPException
from typing import List
# Assume get_db is defined in database.py
# from database import get_db

router = APIRouter(prefix="/api/metrics", tags=["metrics"])

@router.get("/commits", response_model=MetricResponse)
def get_commit_metrics(repo_url: str, db = Depends(get_db)):
    try:
        # Business logic goes here (call pure functions from core/)
        # Example mock data:
        data = [{"hash": "abc1234", "author": "Alice", "lines_added": 50, "lines_removed": 10, "timestamp": "2026-10-20T10:00:00Z"}]
        return MetricResponse(success=True, data=data)
    except Exception as e:
        # Never crash the server, return structured error
        return MetricResponse(success=False, error=str(e))
```