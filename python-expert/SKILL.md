---
name: python-expert
version: 0.1.0
description: Senior Python development skill. Write idiomatic, production-grade Python with type hints, PEP 8, dataclasses, async patterns, and rigorous error handling. Code review and refactoring included.
activation:
  patterns:
    - "python.*code"
    - "write.*python"
    - "python.*script"
    - "debug.*python"
    - "refactor.*python"
    - "python.*class"
    - "python.*async"
    - "python.*api"
  keywords:
    - "python"
    - "py"
    - "pandas"
    - "fastapi"
    - "flask"
    - "django"
    - "asyncio"
    - "dataclass"
    - "pydantic"
    - "pytest"
    - "pip"
    - "venv"
    - "type hint"
    - "decorator"
  max_context_tokens: 3000
---

# Python Expert Skill

You write production-grade Python as a senior engineer. Every snippet you produce follows these standards.

## Code Standards

### Type Hints (mandatory)
```python
from typing import Optional, List, Dict, Union, Any
from dataclasses import dataclass, field

def process_items(items: List[str], limit: Optional[int] = None) -> Dict[str, Any]:
    ...
```

### PEP 8
- 4-space indentation, no tabs
- Max 88 chars per line (Black formatter standard)
- Two blank lines between top-level definitions
- One blank line between methods
- snake_case for variables/functions, PascalCase for classes, UPPER_CASE for constants

### Dataclasses over dicts
```python
@dataclass
class Opportunity:
    name: str
    score: int
    margin: float
    tags: List[str] = field(default_factory=list)
```

### Error Handling
```python
import logging
logger = logging.getLogger(__name__)

try:
    result = fetch_data(url)
except httpx.TimeoutException:
    logger.warning("Timeout fetching %s, retrying...", url)
    raise
except Exception as e:
    logger.error("Unexpected error: %s", e, exc_info=True)
    raise RuntimeError(f"Failed to fetch data: {e}") from e
```

### Async Patterns
```python
import asyncio
import httpx

async def fetch_all(urls: List[str]) -> List[dict]:
    async with httpx.AsyncClient(timeout=30) as client:
        tasks = [client.get(url) for url in urls]
        responses = await asyncio.gather(*tasks, return_exceptions=True)
    return [r.json() for r in responses if not isinstance(r, Exception)]
```

## Preferred Libraries
| Task | Library |
|------|---------|
| HTTP requests | `httpx` (async) or `requests` (sync) |
| Data validation | `pydantic` v2 |
| CLI tools | `typer` |
| Web APIs | `fastapi` |
| Data wrangling | `pandas`, `polars` |
| Scheduling | `apscheduler` |
| Testing | `pytest`, `pytest-asyncio` |
| Env vars | `python-dotenv` |

## Code Review Checklist
Before submitting any Python code, verify:
- [ ] All functions have type hints
- [ ] All exceptions are caught specifically (no bare `except:`)
- [ ] Logging uses `%s` formatting, not f-strings (lazy evaluation)
- [ ] No hardcoded credentials — use env vars or config files
- [ ] Functions do one thing (single responsibility)
- [ ] No global mutable state
- [ ] Docstrings on public functions (Google style)
- [ ] Tests exist or are outlined

## Common Patterns for IronClaw Tasks

### Web scraping with retry
```python
import httpx
from tenacity import retry, stop_after_attempt, wait_exponential

@retry(stop=stop_after_attempt(3), wait=wait_exponential(min=1, max=10))
async def scrape(url: str) -> str:
    async with httpx.AsyncClient() as client:
        response = await client.get(url, headers={"User-Agent": "Mozilla/5.0"})
        response.raise_for_status()
        return response.text
```

### API client with auth
```python
import os
import httpx
from pydantic import BaseModel

class APIClient:
    def __init__(self) -> None:
        self.base_url = os.environ["API_BASE_URL"]
        self.api_key = os.environ["API_KEY"]
        self._client = httpx.AsyncClient(
            base_url=self.base_url,
            headers={"Authorization": f"Bearer {self.api_key}"},
            timeout=30,
        )

    async def get(self, path: str, **params: Any) -> dict:
        response = await self._client.get(path, params=params)
        response.raise_for_status()
        return response.json()
```

### CLI entry point
```python
import typer

app = typer.Typer()

@app.command()
def main(
    topic: str = typer.Argument(..., help="Research topic"),
    limit: int = typer.Option(10, help="Max results"),
    verbose: bool = typer.Option(False, "--verbose", "-v"),
) -> None:
    """IronClaw research tool."""
    ...

if __name__ == "__main__":
    app()
```
