---
tags: ["shell-linux", "system", "llama", "cuda", "ai", "install"]
---
# Install llama-cpp-python with CUDA (GPU)

Installs `llama-cpp-python` with CUDA support so local LLMs use the GPU instead of CPU-only inference.

Paste and run directly in the terminal — no file needed.

## Command

### Option 1 — using CMAKE_ARGS (recommended)

```bash
CMAKE_ARGS="-DLLAMA_CUBLAS=on" pip install --force-reinstall --no-cache-dir llama-cpp-python
```

### Option 2 — via extras (may not work on all versions)

```bash
pip install "llama-cpp-python[cuda]" --force-reinstall --no-cache-dir
```

### Verify CUDA is being used

```python
from llama_cpp import Llama

# n_gpu_layers: number of layers to offload to GPU (-1 = all)
llm = Llama(model_path="./model.gguf", n_gpu_layers=-1)
result = llm("Hello, world!")
print(result["choices"][0]["text"])
```

---

## Prerequisites

- NVIDIA GPU with CUDA Toolkit installed (`nvcc --version`)
- Compatible driver: `nvidia-smi` should work before attempting this
- Python 3.9+

---

## Troubleshoot

```bash
# Check CUDA toolkit
nvcc --version

# Confirm GPU is visible
nvidia-smi

# Rebuild from source (if wheel fails)
pip install --no-binary :all: --force-reinstall llama-cpp-python \
  CMAKE_ARGS="-DLLAMA_CUBLAS=on"
```

---

## Notes

- `--force-reinstall --no-cache-dir` is required to pick up the new CUDA build — pip may otherwise restore a cached CPU-only version.
- On Windows, the CUDA Toolkit installer must add `nvcc` to `PATH` before running pip.
