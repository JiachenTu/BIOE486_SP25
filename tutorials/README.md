```markdown
# Fine‑tune SAM (Segment Anything) – Tutorial Notebook

This folder contains a single Jupyter notebook, **`Fine_tune_SAM.ipynb`**, that walks you through fine‑tuning Meta AI’s *Segment Anything Model* on a small, custom dataset.

> **Prerequisite:**  
> Make sure you have completed the *BIOE 486 Environment Setup Tutorial* in the course repository.  
> If you followed those steps, all required Python packages are already installed inside your `bioe486` virtual environment.

---

## 1 · Get the code

```bash
# clone the main course repo (if you haven't yet)
git clone https://github.com/JiachenTu/BIOE486_SP25.git
cd BIOE486_SP25/tutorials/   # ← this folder
```

---

## 2 · Activate the course environment

```bash
# Linux / macOS
source $HOME/bioe486/venv/bioe486/bin/activate

# (Optional) confirm you have a GPU:
python - <<'PY'
import torch, pynvml, os
print("CUDA available:", torch.cuda.is_available())
if torch.cuda.is_available():
    pynvml.nvmlInit()
    print("Using GPU:", torch.cuda.current_device())
PY
```

---

## 3 · Launch Jupyter

Choose **one** of the two options below.

<details>
<summary><strong>JupyterLab (recommended)</strong></summary>

```bash
jupyter lab --no-browser --port=8888 --notebook-dir="$(pwd)"
```

* Copy the URL with the token from the terminal into your browser  
  (or use SSH port‑forwarding if you’re on a remote server).

</details>

<details>
<summary><strong>Classic Jupyter Notebook</strong></summary>

```bash
jupyter notebook --no-browser --port=8888 --notebook-dir="$(pwd)"
```

</details>

Once the interface opens, click **`Fine_tune_SAM.ipynb`** and run the cells top‑to‑bottom.

---

## 4 · Troubleshooting

| Symptom | Fix |
|---------|-----|
| **Module not found** | Double‑check that your `bioe486` environment is activated. |
| **CUDA out of memory** | Lower the `batch_size` in the notebook (default = 2) or switch to a GPU with more VRAM. |
| **Permission denied saving checkpoints** | Save outputs to your personal shared folder:<br>`/shared/BIOE486/SP25/users/$USER/…` |

---

Happy segmenting!  
```
