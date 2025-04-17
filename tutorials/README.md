# Fine‑tune SAM (Segment Anything) – Tutorial Notebook

This notebook guides you through fine‑tuning Meta AI's *Segment Anything Model* on a custom dataset.

> **⚠️ Prerequisites:**  
> - Complete the *BIOE 486 Environment Setup Tutorial* in the course repository
> - All required Python packages should already be installed in your `bioe486` virtual environment

## 📋 Step-by-Step Guide

### 1️⃣ Get the code

```bash
# Clone the main course repo (if you haven't yet)
git clone https://github.com/JiachenTu/BIOE486_SP25.git
cd BIOE486_SP25/tutorials/   # ← this folder
```

### 2️⃣ Activate the course environment

```bash
# Linux / macOS
source $HOME/bioe486/venv/bioe486/bin/activate

# (Optional) Verify GPU availability:
python - <<'PY'
import torch, pynvml, os
print("CUDA available:", torch.cuda.is_available())
if torch.cuda.is_available():
    pynvml.nvmlInit()
    print("Using GPU:", torch.cuda.current_device())
PY
```

### 3️⃣ Launch Jupyter

Choose **one** of the options below:

<details>
<summary><b>🚀 JupyterLab (recommended)</b></summary>

```bash
jupyter lab --no-browser --port=8888 --notebook-dir="$(pwd)"
```

* Copy the URL with the token from the terminal into your browser
* Or use SSH port‑forwarding if you're on a remote server
</details>

<details>
<summary><b>📓 Classic Jupyter Notebook</b></summary>

```bash
jupyter notebook --no-browser --port=8888 --notebook-dir="$(pwd)"
```
</details>

Once Jupyter opens, select **`Fine_tune_SAM.ipynb`** and execute the cells sequentially.

### 4️⃣ Troubleshooting

| Issue | Solution |
|-------|----------|
| **Module not found** | Ensure your `bioe486` environment is activated |
| **CUDA out of memory** | Reduce `batch_size` in the notebook (default = 2) or use a GPU with more VRAM |
| **Permission denied saving checkpoints** | Save outputs to your personal shared folder:<br>`/shared/BIOE486/SP25/users/$USER/...` |

---

## 📊 Expected Outputs

The notebook will produce:
- Fine-tuned SAM model checkpoints
- Visualization of segmentation results
- Performance metrics on your custom dataset