# 🚀 BIOE486 (Spring 2025) – Environment Setup Tutorial

This guide shows you how to create a **clean, conflict‑free Python machine‑learning (ML) environment** for BIOE486.

> **Key policy for Spring 2025**  
> • **Virtual environments live in your home directory** (quota ≈ 25 GB).  
> • **Datasets, checkpoints, and experiment logs live in the class shared space** to save home‑quota space.

---

## 📌 Table of Contents
1. [Overview & Storage Policy](#overview--storage-policy)  
2. [Step‑by‑Step Setup](#step-by-step-setup)  
   ▪ [Create Personal Workspace Folders](#create-personal-workspace-folders)  
   ▪ [Create Python Virtual Environment](#create-python-virtual-environment)  
   ▪ [Activate Virtual Environment](#activate-virtual-environment)  
   ▪ [Upgrade *pip*](#upgrade-pip)  
   ▪ [Install GPU‑enabled PyTorch](#install-gpu-enabled-pytorch)  
   ▪ [Install Other ML Packages](#install-other-ml-packages)  
   ▪ [Good vs. Bad Installation Examples](#good-vs-bad-installation-examples)  
   ▪ [Verify PyTorch](#verify-pytorch)  
   ▪ [Run Jupyter Notebooks](#run-jupyter-notebooks)  
   ▪ [Deactivate Environment](#deactivate-environment)  
3. [Dataset & Log Storage](#dataset--log-storage)  
4. [Common Issues & Troubleshooting](#common-issues--troubleshooting)  
5. [Quick Reference](#quick-reference)

---

## 📌 Overview & Storage Policy

### What are `$HOME` and `$USER`?
* **`$HOME`** is the absolute path to *your* home directory (e.g. `/home/abc123`).  
* **`$USER`** is your login name or NetID (e.g. `abc123`).  
We use these variables for brevity—replace them with the actual values shown on your account.

| Area | Location | Purpose |
|------|----------|---------|
| **Home directory** | `$HOME` | Source code, **virtual environments**, small config files (quota ≈ 25 GB). |
| **Class shared space** | `/shared/BIOE486/SP25/` | Large datasets, model checkpoints, TensorBoard logs, other heavy outputs. |

**Golden Rules**
1. **Install Python packages only inside your activated virtual‑env**—never system‑wide.
2. **Keep large files out of `$HOME`**; store them in `/shared/BIOE486/SP25/users/$USER/`.
3. **Respect classmates’ data**: do not modify or delete anything outside your own sub‑folder.

---

## 🛠 Step‑by‑Step Setup

### ✅ Create Personal Workspace Folders
```bash
# In your *home* directory – code & virtual‑env
mkdir -p "$HOME/bioe486/code"
mkdir -p "$HOME/bioe486/venv"

# In the *shared* space – heavy data
mkdir -p /shared/BIOE486/SP25/users/$USER/datasets
mkdir -p /shared/BIOE486/SP25/users/$USER/logs
```

---

### ✅ Create Python Virtual Environment
```bash
python3 -m venv "$HOME/bioe486/venv/env"
```

---

### ✅ Activate Virtual Environment
```bash
source "$HOME/bioe486/venv/env/bin/activate"
# Prompt now shows (env)
```

---

### ✅ Upgrade *pip*
```bash
pip install --upgrade pip
```

---

### ✅ Install GPU‑enabled PyTorch
```bash
pip install torch torchvision torchaudio
```

---

### ✅ Install Other ML Packages
```bash
pip install numpy pandas matplotlib scikit-learn jupyter
```

---

### ⚠️ Good vs. Bad Installation Examples
| | **Good** | **Bad** |
|---|---|---|
| **Activate env first** | `source "$HOME/bioe486/venv/env/bin/activate"`<br>`pip install matplotlib` | `pip install matplotlib` *(without activation)* |
| **Never use sudo** | — | `sudo pip install matplotlib` |
| **Location** | packages installed inside `$HOME/bioe486/venv/env` | packages scattered in system Python, affecting everyone |

---

### ✅ Verify PyTorch
```bash
python - <<'PY'
import torch
print('PyTorch version:', torch.__version__)
print('CUDA available  :', torch.cuda.is_available())
PY
```

---

### ✅ Run Jupyter Notebooks
```bash
mkdir -p "$HOME/bioe486/notebooks"

jupyter notebook \
  --no-browser \
  --port=8888 \
  --notebook-dir="$HOME/bioe486/notebooks"
```
Follow instructor instructions for port‑forwarding or remote access.

---

### ✅ Deactivate Environment
```bash
deactivate
```

---

## 📁 Dataset & Log Storage
```
/shared/BIOE486/SP25/users/$USER/datasets/   # raw & processed datasets
/shared/BIOE486/SP25/users/$USER/logs/       # TensorBoard runs, model ckpts
```
* Check `/shared/BIOE486/SP25/datasets/common/` before downloading duplicates.
* Use clear names like `cifar10/`, `brats2021/`, `exp1_resnet50/`.
* Clean up obsolete logs & checkpoints at the end of each project.

---

## 🚧 Common Issues & Troubleshooting

### “No space left on device” during `pip install`
```
error: could not create 'build/lib/transformers/models/detr': No space left on device
```
🔧 **Problem**: The disk (or the temporary directory used by *pip*) is full.

**Fix**: Point `pip` to a temporary folder inside your home directory with enough space:
```bash
export TMPDIR=$HOME/tmp
mkdir -p "$TMPDIR"
```
Example (replace `$USER` with your NetID):
```bash
export TMPDIR=/home/$USER/tmp
```
Then re‑run `pip install …`.

---

## 📌 Quick Reference
| Task | Command |
|------|---------|
| Create virtual‑env | `python3 -m venv "$HOME/bioe486/venv/env"` |
| Activate | `source "$HOME/bioe486/venv/env/bin/activate"` |
| Upgrade pip | `pip install --upgrade pip` |
| Install PyTorch | `pip install torch torchvision torchaudio` |
| Install ML pkgs | `pip install numpy pandas matplotlib scikit-learn jupyter` |
| Launch Jupyter | `jupyter notebook --no-browser --port=8888 --notebook-dir="$HOME/bioe486/notebooks"` |
| Shared data root | `/shared/BIOE486/SP25/users/$USER/datasets` |
| Shared logs root | `/shared/BIOE486/SP25/users/$USER/logs` |
| Deactivate env | `deactivate` |

---

