---
tags: ["shell-linux", "system", "ollama", "llm", "ai"]
---
# Run a Local LLM with Ollama

Installs Ollama, pulls a model, and runs it locally — no cloud API or GPU required for smaller models.

Paste and run directly in the terminal — no file needed.

## Install

```bash
# Linux (official installer)
curl -fsSL https://ollama.com/install.sh | sh
```

## Command

### Pull and run a model interactively

```bash
ollama run mistral
```

```bash
ollama run codellama:7b
```

```bash
ollama run llama3
```

### List downloaded models

```bash
ollama list
```

### Start the server (background)

```bash
ollama serve
```

> The API listens on `http://localhost:11434` by default.

---

## HTTP API

### Generate a completion

```bash
curl http://localhost:11434/api/generate \
  -d '{
    "model": "mistral",
    "prompt": "Write a Python function that reverses a string",
    "stream": false
  }'
```

### List available models via API

```bash
curl http://localhost:11434/api/tags
```

---

## Popular models

| Model | Size | Best for |
|-------|------|----------|
| `mistral` | ~4 GB | General chat, code |
| `codellama:7b` | ~4 GB | Code generation |
| `llama3` | ~5 GB | General purpose |
| `phi3` | ~2 GB | Lightweight, fast |
| `deepseek-coder` | ~4 GB | Code / debugging |
