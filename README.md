# 🚀 BIOE486 (Spring 2025) – Environment Setup Tutorial

This guide will help you create a **clean, conflict-free Python machine learning (ML) environment** for BIOE486.

> **🔑 Key Policy for Spring 2025**  
> - **Virtual environments** must be stored in your home directory (quota ≈ 25 GB)
> - **Datasets, checkpoints, and experiment logs** must be stored in the class shared space

## 📌 Table of Contents

1. [Overview & Storage Policy](#overview--storage-policy)  
2. [Environment Setup](#environment-setup)  
   - [Creating Workspace Folders](#creating-workspace-folders)  
   - [Setting Up Python Virtual Environment](#setting-up-python-virtual-environment)  
   - [Activating Your Environment](#activating-your-environment)  
   - [Installing Required Packages](#installing-required-packages)  
   - [Verifying Your Installation](#verifying-your-installation)
3. [Working with Jupyter Notebooks](#working-with-jupyter-notebooks)
4. [Dataset & Log Storage Guidelines](#dataset--log-storage-guidelines)  
5. [Troubleshooting Common Issues](#troubleshooting-common-issues)  
6. [Quick Reference Commands](#quick-reference-commands)

---

## Overview & Storage Policy

### Environment Variables

Throughout this guide, we'll use these variables for brevity:
- **`$HOME`**: The absolute path to your home directory (e.g., `/home/abc123`)
- **`$USER`**: Your login name/NetID (e.g., `abc123`)

Replace these with your actual values as needed.

### Storage Allocation

| Location | Purpose | Quota |
|----------|---------|-------|
| **Home Directory** (`$HOME`) | Source code, virtual environments, config files | ~25 GB |
| **Class Shared Space** (`/shared/BIOE486/SP25/`) | Datasets, model checkpoints, TensorBoard logs | Shared |

### Critical Guidelines

1. **Always install Python packages within your activated virtual environment** — never system-wide
2. **Store large files in the shared space** (`/shared/BIOE486/SP25/users/$USER/`)
3. **Respect other students' data** — don't modify or delete anything outside your folder

---

## Environment Setup

### Creating Workspace Folders

First, let's create the necessary directory structure:

```bash
# 1) Home directory folders (for code & virtual environment)
mkdir -p "$HOME/bioe486/code"
mkdir -p "$HOME/bioe486/venv"

# 2) Shared space folders (for datasets & logs)
mkdir -p /shared/BIOE486/SP25/users/$USER/datasets
mkdir -p /shared/BIOE486/SP25/users/$USER/logs
```

### Setting Up Python Virtual Environment

A virtual environment provides an isolated Python installation where you can install packages without affecting the system or other users.

```bash
# Create a new environment named 'bioe486'
python3 -m venv "$HOME/bioe486/venv/bioe486"
```

This creates a folder containing:
- `bin/` (Python executables, pip, etc.)
- `lib/` (installed packages)
- Other configuration files

**Optional:** Add a convenient alias to your shell startup file (`.bashrc` or `.zshrc`):

```bash
echo 'alias acbioe486="source $HOME/bioe486/venv/bioe486/bin/activate"' >> ~/.bashrc
```

After reloading your configuration (`source ~/.bashrc`), you can simply type `acbioe486` to activate your environment.

### Activating Your Environment

Before installing packages or running Python code, always activate your environment:

```bash
source "$HOME/bioe486/venv/bioe486/bin/activate"
```

Your prompt should now show `(bioe486)` at the beginning, indicating you're working within your isolated environment.

### Installing Required Packages

Once your environment is activated:

1. **Upgrade pip** (the package installer):
   ```bash
   pip install --upgrade pip
   ```

2. **Install PyTorch** with GPU support:
   ```bash
   pip install torch torchvision torchaudio
   ```

3. **Install core ML libraries**:
   ```bash
   pip install numpy pandas matplotlib scikit-learn jupyterlab
   pip install git+https://github.com/huggingface/transformers.git
   pip install datasets
   pip install monai
   ```

#### ⚠️ Installation Best Practices

| Correct Approach | Incorrect Approach |
|------------------|-------------------|
| Activate environment first, then install packages | Install packages without activating environment |
| `pip install package_name` | `sudo pip install package_name` (NEVER use sudo) |
| All packages contained within your virtual environment | Packages installed system-wide |

### Verifying Your Installation

Test your PyTorch installation and GPU availability:

```bash
python - <<'PY'
import torch
print("PyTorch version:", torch.__version__)
print("CUDA available:", torch.cuda.is_available())
PY
```

You should see `CUDA available: True` if GPU acceleration is accessible.

---

## Working with JupyterLab

Store your notebooks in your home directory where they can access your virtual environment:

```bash
# Create a notebooks directory
mkdir -p "$HOME/bioe486/notebooks"

# Launch JupyterLab server
jupyter lab --no-browser --port=8888 --notebook-dir="$HOME/bioe486/notebooks"
```

Follow your instructor's guidance for remote access or port forwarding if needed.

When finished with your work, deactivate your environment:

```bash
deactivate
```

---

## Dataset & Log Storage Guidelines

Always store large files in the shared class space:

```
/shared/BIOE486/SP25/users/$USER/datasets/   # For raw & processed datasets
/shared/BIOE486/SP25/users/$USER/logs/       # For experiment outputs
```

### Best Practices

- Check `/shared/BIOE486/SP25/datasets/common/` before downloading datasets that might already exist
- Use descriptive naming conventions (e.g., `cifar10/`, `resnet50_experiment1/`)
- Clean up unused files regularly to conserve shared space

---

## Troubleshooting Common Issues

### "No space left on device" Error

If you encounter this error during package installation:

```
error: could not create 'build/lib/transformers/models/detr': No space left on device
```

**Solution:** Redirect pip's temporary directory to your home folder:

```bash
# Create a temporary directory with sufficient space
export TMPDIR=$HOME/tmp
mkdir -p "$TMPDIR"

# Then retry your pip install command
pip install [package-name]
```

---

## Quick Reference Commands

| Task | Command |
|------|---------|
| **Create virtual environment** | `python3 -m venv "$HOME/bioe486/venv/bioe486"` |
| **Activate environment** | `source "$HOME/bioe486/venv/bioe486/bin/activate"` |
| **Upgrade pip** | `pip install --upgrade pip` |
| **Install PyTorch** | `pip install torch torchvision torchaudio` |
| **Install ML packages** | `pip install numpy pandas matplotlib scikit-learn jupyterlab datasets monai git+https://github.com/huggingface/transformers.git` |
| **Launch JupyterLab** | `jupyter lab --no-browser --port=8888 --notebook-dir="$HOME/bioe486/notebooks"` |
| **Access personal datasets** | `/shared/BIOE486/SP25/users/$USER/datasets` |
| **Access personal logs** | `/shared/BIOE486/SP25/users/$USER/logs` |
| **Deactivate environment** | `deactivate` |

---

**Happy ML coding — see you in class!**
