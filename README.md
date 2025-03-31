
# 🚀 BIOE486 (Spring 2025) - Environment Setup Tutorial

This document helps you set up an efficient, scalable, and conflict-free Python Machine Learning (ML) environment for BIOE486, focusing on PyTorch and related ML tools.

---

## 📌 **Table of Contents**

1. [Overview and Important Guidelines](#overview-and-important-guidelines)
2. [Step-by-Step Setup Instructions](#step-by-step-setup-instructions)
    - [Create Personal Working Directory](#create-personal-working-directory)
    - [Create Python Virtual Environment](#create-python-virtual-environment)
    - [Activate Virtual Environment](#activate-virtual-environment)
    - [Upgrade pip](#upgrade-pip)
    - [Install PyTorch (GPU-enabled)](#install-pytorch-gpu-enabled)
    - [Install Other Essential ML Packages](#install-other-essential-ml-packages)
    - [Good vs. Bad Package Installation Examples](#good-vs-bad-package-installation-examples)
    - [Verify PyTorch Installation](#verify-pytorch-installation)
    - [Run Jupyter Notebooks](#run-jupyter-notebooks)
    - [Deactivate Environment](#deactivate-environment)
3. [Dataset Sharing Guidelines](#dataset-sharing-guidelines)
4. [Common Issues and Troubleshooting](#common-issues-and-troubleshooting)

---

## 📌 Overview and Important Guidelines

Due to limited space in the `/home` directory, **all students must work in the shared directory**:

```
/shared/BIOE486/SP25/
```

**IMPORTANT RULES:**

- **Always use your own folder (`$USER`)** within this shared directory.
- **NEVER modify or delete other users' folders or files** to avoid conflicts.
- **Share common datasets** in the designated shared dataset directory (`/shared/BIOE486/SP25/dataset`).

---

## 🛠 Step-by-Step Setup Instructions

### ✅ **Create Personal Working Directory**

Use your login username (`$USER`) to create your own workspace:

```bash
mkdir -p /shared/BIOE486/SP25/users/$USER
mkdir -p /shared/BIOE486/SP25/venvs/$USER
```

Verify your username:

```bash
echo $USER
```

---

### ✅ **Create Python Virtual Environment**

Run this command to create your own Python virtual environment (`env`):

```bash
python3 -m venv /shared/BIOE486/SP25/venvs/$USER/env
```

---

### ✅ **Activate Virtual Environment**

Activate your virtual environment each time you work:

```bash
source /shared/BIOE486/SP25/venvs/$USER/env/bin/activate
```

Your terminal prompt will now start with `(env)`.

---

### ✅ **Upgrade pip**

After activating your environment, upgrade pip immediately:

```bash
pip install --upgrade pip
```

Always upgrade pip if prompted.

---

### ✅ **Install PyTorch (GPU-enabled)**

Our system has GPUs available. Install GPU-enabled PyTorch easily with:

```bash
pip3 install torch torchvision torchaudio
```

---

### ✅ **Install Other Essential ML Packages**

Install additional essential ML packages:

```bash
pip install numpy pandas matplotlib scikit-learn jupyter
```

---

### ⚠️ **Good vs. Bad Package Installation Examples**

To avoid conflicts and issues, carefully follow the correct practice:

- **✅ GOOD Example (Correct Practice)**

```bash
# Activate your virtual environment first
source /shared/BIOE486/SP25/venvs/$USER/env/bin/activate

# Install within your activated environment
pip install matplotlib
```

- **❌ BAD Example (Incorrect Practice)**

```bash
# Never install packages directly (without activation)
pip install matplotlib
```

or

```bash
# Never use sudo or global installs
sudo pip install matplotlib
```

Incorrect methods affect everyone's environment and can cause conflicts.

---

### ✅ **Verify PyTorch Installation**

Check your installation and GPU availability:

```bash
python
```

Within Python, run:

```python
import torch
print(f"PyTorch version: {torch.__version__}")
print(f"CUDA (GPU) Available: {torch.cuda.is_available()}")
```

Example Output:

```
PyTorch version: 2.3.0
CUDA (GPU) Available: True
```

Exit Python with:

```python
exit()
```

---

### ✅ **Run Jupyter Notebooks**

Create your own notebooks directory and start Jupyter Notebook:

```bash
mkdir -p /shared/BIOE486/SP25/users/$USER/notebooks

jupyter notebook --no-browser --port=8888 --notebook-dir=/shared/BIOE486/SP25/users/$USER/notebooks
```

Follow instructor-provided instructions for remote browser access.

---

### ✅ **Deactivate Environment**

When finished, deactivate your environment:

```bash
deactivate
```

---

## 📁 Dataset Sharing Guidelines

You are encouraged to share common datasets. Store them clearly labeled within:

```
/shared/BIOE486/SP25/dataset
```

- Check existing datasets first to avoid duplicates.
- Clearly name and document datasets so others can understand and use them easily.

Example of good practice:

```
/shared/BIOE486/SP25/dataset/cifar10/
/shared/BIOE486/SP25/dataset/human-cell-images/
```

---

## 🚧 Common Issues and Troubleshooting

- **Permission Denied Issues:** Immediately notify the instructor or TA.
- **GPU Not Available:** Ensure you used the correct installation command and verify with the PyTorch installation verification step.
- **Limited Space Errors:** Report to the instructor right away.

---

## 📌 **Quick Reference Summary Table**

| Task                                      | Command                                    |
|-------------------------------------------|--------------------------------------------|
| Create workspace                          | `mkdir -p /shared/BIOE486/SP25/users/$USER` |
| Create Python environment                 | `python3 -m venv /shared/BIOE486/SP25/venvs/$USER/env` |
| Activate Python environment               | `source /shared/BIOE486/SP25/venvs/$USER/env/bin/activate` |
| Upgrade pip                               | `pip install --upgrade pip`                |
| Install GPU-enabled PyTorch               | `pip3 install torch torchvision torchaudio`|
| Install ML packages                       | `pip install numpy pandas matplotlib scikit-learn jupyter` |
| Run Jupyter                               | `jupyter notebook --no-browser --port=8888 --notebook-dir=/shared/BIOE486/SP25/users/$USER/notebooks` |
| Deactivate environment                    | `deactivate`                               |


---

## 🎯 **Final Reminders**

- Always work and install packages within your activated virtual environment.
- Maintain your workspace clean and avoid modifying others’ environments.
- Share datasets thoughtfully in the provided shared directory.

---

**Happy ML coding, and enjoy BIOE486! 🚀**
