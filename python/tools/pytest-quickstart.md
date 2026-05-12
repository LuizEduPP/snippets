---
tags: ["python", "tools", "pytest", "testing"]
---
# pytest Quickstart

Minimal setup to write and run Python tests with pytest, including VS Code integration.

## Dependencies

```bash
pip install pytest
```

## Code

### Basic test structure

```python
# tests/test_math.py

def add(a, b):
    return a + b

def test_add():
    assert add(1, 2) == 3
    assert add(-1, 1) == 0
    assert add(-1, -1) == -2
```

### Run tests

```bash
pytest                        # run all tests
pytest tests/                 # run tests in folder
pytest -v                     # verbose output
pytest -k "test_add"          # run tests matching name
pytest --tb=short             # shorter traceback
```

### Project structure

```
project/
├── app/
│   └── math.py
└── tests/
    ├── __init__.py
    └── test_math.py
```

### Fixtures

```python
import pytest

@pytest.fixture
def sample_data():
    return {"name": "Alice", "age": 30}

def test_name(sample_data):
    assert sample_data["name"] == "Alice"
```

### Parametrize

```python
@pytest.mark.parametrize("a,b,expected", [
    (1, 2, 3),
    (0, 0, 0),
    (-1, 1, 0),
])
def test_add_parametrized(a, b, expected):
    assert add(a, b) == expected
```

---

## VS Code — enable pytest

Add to `.vscode/settings.json`:

```json
{
    "python.testing.pytestEnabled": true,
    "python.testing.pytestArgs": ["tests"],
    "python.testing.unittestEnabled": false
}
```
