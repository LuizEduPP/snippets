---
tags: ["python", "dev-tools", "testing", "pytest"]
---
# Pytest Minimal Quickstart

A highly explicit functional approach to cleanly structuring decoupled chunks of testing logic in Python without the extreme boilerplate rigidity of the heavy built-in `unittest` class module.

## 🛠️ How it works under the hood

1. **`assert` Magic**: Pytest completely intercepts and overrides standard Python `assert` behavior. Instead of just throwing a silent `AssertionError`, it intelligently dumps exactly what variables and parameters led to the logic failing on an internal AST level.
2. **`@pytest.fixture`**: A declarative decorator that instantiates mock data (like dummy arrays, simulated Databases, or JSON payloads) reliably and pipes those dictionaries right into testing parameter scopes sequentially.
3. **`@pytest.mark.parametrize`**: Destroys verbose `for` loop testing configurations. Instead, this decorator injects immense tuple arrays of unique dynamic inputs testing directly against isolated expected matrix outputs automatically scaling.

---

## ⚡ Setup / Installation

Install the library:
```bash
pip install pytest
```

---

## 🚀 Usage Guide

### Defining the Root Basic Project Architecture
Do not stray from the `test_*.py` and `*_test.py` naming topology. Pytest traverses folders relying exactly on this hardcoded metadata marker to build lists of actionable routines.

```
project/
├── app/
│ └── math.py
└── tests/
 ├── __init__.py
 └── test_math.py
```

### Implementing Parameter Iterations
File: `tests/test_math.py`

```python
import pytest

# Abstract simple code simulating an app logic
def sum_values(a, b):
 return a + b

# A simple mock variable payload
@pytest.fixture
def dummy_db_payload():
 return {"id": "1152A", "status": "ACTIVE"}

# 1. Run basic raw AST overrides
def test_static_properties(dummy_db_payload):
 assert dummy_db_payload["status"] == "ACTIVE"

# 2. Iterate heavily across vast matrix combinations directly
@pytest.mark.parametrize("value_a, value_b, expected_output", [
 (1, 2, 3),
 (0, 0, 0),
 (-1, 1, 0),
 (500, -100, 400)
])
def test_add_parametrized(value_a, value_b, expected_output):
 assert sum_values(value_a, value_b) == expected_output
```

### Executing Actions via Terminal

```bash
# Sweep the folder recursively and run all tests immediately
pytest tests/

# Execute with verbose step-by-step stdout printing
pytest -v

# Filter exactly one specific method string and run it isolatedly
pytest -k "test_add_parametrized"
```

## 🐛 Troubleshooting in VS Code
If VS Code's testing tab pane isn't rendering your tests, manually override the embedded configurations. Inject this into `.vscode/settings.json`:

```json
{
 "python.testing.pytestEnabled": true,
 "python.testing.pytestArgs": ["tests"],
 "python.testing.unittestEnabled": false
}
```
