# Miniconda Python 3.12 Setup

Complete Python environment setup for **Ubuntu Linux**, **Data Science**, **Machine Learning**, **Deep Learning**, **LLM development**, **PyTorch**, **Jupyter**, and **VS Code**.

---

## System Configuration

| Component               | Setup                |
| ----------------------- | -------------------- |
| OS                      | Ubuntu Linux         |
| Environment Manager     | Miniconda            |
| Conda Environment       | `py312`              |
| Python                  | 3.12                 |
| IDE                     | VS Code              |
| Notebook                | Jupyter / JupyterLab |
| GPU                     | NVIDIA RTX 2050 4 GB |
| NVIDIA Driver           | 595.84               |
| CUDA reported by driver | 13.2                 |

---

# 1. Install Miniconda

Download Miniconda:

```bash
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
```

Run the installer:

```bash
bash Miniconda3-latest-Linux-x86_64.sh
```

Accept the license and allow the installer to initialize Conda.

If Conda was not initialized automatically:

```bash
~/miniconda3/bin/conda init bash
```

Reload the shell:

```bash
source ~/.bashrc
```

Verify:

```bash
conda --version
```

---

# 2. Create Python 3.12 Environment

Create the environment:

```bash
conda create -n py312 python=3.12 -y
```

Activate it:

```bash
conda activate py312
```

Verify Python:

```bash
python --version
```

Expected:

```text
Python 3.12.x
```

Check the active environment:

```bash
conda info --envs
```

The active environment will have `*` beside:

```text
py312
```

---

# 3. Upgrade pip

Always upgrade pip inside the environment:

```bash
python -m pip install --upgrade pip
```

Verify:

```bash
pip --version
```

Check which Python is being used:

```bash
which python
```

Expected path:

```text
/home/<username>/miniconda3/envs/py312/bin/python
```

---

# 4. Install Core Packages

Install the basic scientific Python stack:

```bash
conda install -y \
numpy \
scipy \
pandas \
matplotlib \
scikit-learn \
jupyter \
jupyterlab \
ipykernel \
openpyxl
```

---

# 5. Install Additional Python Packages

Install commonly used packages:

```bash
pip install \
seaborn \
xgboost \
opencv-python \
Pillow \
tqdm \
requests \
python-dotenv \
joblib \
PyYAML
```

---

# 6. Install PyTorch

Install PyTorch according to the current official PyTorch installation instructions for your operating system and GPU.

Check the installation:

```bash
python -c "import torch; print(torch.__version__)"
```

Check CUDA:

```bash
python -c "import torch; print(torch.cuda.is_available())"
```

If CUDA is available, check the GPU:

```bash
python -c "import torch; print(torch.cuda.get_device_name(0))"
```

Expected GPU:

```text
NVIDIA GeForce RTX 2050
```

Check the CUDA version recognized by PyTorch:

```bash
python -c "import torch; print(torch.version.cuda)"
```

---

# 7. Check NVIDIA GPU

Check the NVIDIA driver:

```bash
nvidia-smi
```

This should display information about:

```text
GPU
Driver Version
CUDA Version
GPU Memory
```

For the current system:

```text
GPU: NVIDIA GeForce RTX 2050
Driver: 595.84
VRAM: 4 GB
```

Note that the CUDA version displayed by `nvidia-smi` is the maximum CUDA runtime compatibility reported by the installed NVIDIA driver. It is not necessarily the CUDA toolkit/runtime bundled with a particular PyTorch build.

---

# 8. Install Transformers and LLM Libraries

For NLP, Transformers, and LLM projects:

```bash
pip install \
transformers \
datasets \
tokenizers \
accelerate \
sentencepiece
```

Verify:

```bash
python -c "import transformers; print(transformers.__version__)"
```

---

# 9. Jupyter Setup

Install the Python kernel:

```bash
python -m ipykernel install \
--user \
--name py312 \
--display-name "Python 3.12 (py312)"
```

Check available kernels:

```bash
jupyter kernelspec list
```

You should see:

```text
python3
py312
```

---

# 10. Start Jupyter Notebook

Activate the environment:

```bash
conda activate py312
```

Start Jupyter Notebook:

```bash
jupyter notebook
```

Or use JupyterLab:

```bash
jupyter lab
```

---

# 11. VS Code Setup

Open the project:

```bash
code .
```

Inside VS Code:

1. Install the **Python** extension.
2. Install the **Jupyter** extension.
3. Open a `.py` or `.ipynb` file.
4. Select the Python interpreter.
5. Choose:

```text
Python 3.12 (py312)
```

For notebooks, select:

```text
Python 3.12 (py312)
```

as the kernel.

Verify inside a notebook:

```python
import sys

print(sys.executable)
print(sys.version)
```

The executable should point to the `py312` Conda environment.

---

# 12. Complete Requirements

Create a `requirements.txt` file:

```text
# Jupyter
jupyter
jupyterlab
ipykernel

# Scientific Computing
numpy
scipy

# Data Analysis
pandas
openpyxl

# Visualization
matplotlib
seaborn

# Machine Learning
scikit-learn
xgboost

# Deep Learning
torch
torchvision
torchaudio

# NLP / Transformers / LLM
transformers
datasets
tokenizers
accelerate
sentencepiece

# Computer Vision
opencv-python
Pillow

# Utilities
tqdm
requests
python-dotenv
joblib
PyYAML
```

Install everything:

```bash
pip install -r requirements.txt
```

---

# 13. Verify All Major Libraries

Run:

```bash
python -c "import numpy; print('NumPy:', numpy.__version__)"
```

```bash
python -c "import pandas; print('Pandas:', pandas.__version__)"
```

```bash
python -c "import sklearn; print('Scikit-learn:', sklearn.__version__)"
```

```bash
python -c "import matplotlib; print('Matplotlib:', matplotlib.__version__)"
```

```bash
python -c "import torch; print('PyTorch:', torch.__version__)"
```

```bash
python -c "import transformers; print('Transformers:', transformers.__version__)"
```

---

# 14. One-Shot Verification

Run:

```bash
python -c "
import sys
import numpy
import pandas
import sklearn
import matplotlib
import torch
import transformers

print('Python:', sys.version)
print('NumPy:', numpy.__version__)
print('Pandas:', pandas.__version__)
print('Scikit-learn:', sklearn.__version__)
print('Matplotlib:', matplotlib.__version__)
print('PyTorch:', torch.__version__)
print('Transformers:', transformers.__version__)
print('CUDA Available:', torch.cuda.is_available())

if torch.cuda.is_available():
    print('GPU:', torch.cuda.get_device_name(0))
    print('PyTorch CUDA:', torch.version.cuda)
"
```

---

# 15. Conda Environment Commands

### List environments

```bash
conda env list
```

or:

```bash
conda info --envs
```

### Activate environment

```bash
conda activate py312
```

### Deactivate environment

```bash
conda deactivate
```

### Create another environment

```bash
conda create -n myenv python=3.12 -y
```

### Remove an environment

```bash
conda remove -n myenv --all
```

### Clone an environment

```bash
conda create -n py312-copy --clone py312
```

---

# 16. Package Management

Install using Conda:

```bash
conda install <package>
```

Install using pip:

```bash
pip install <package>
```

Update a Conda package:

```bash
conda update <package>
```

Update a pip package:

```bash
pip install --upgrade <package>
```

Show installed Conda packages:

```bash
conda list
```

Show installed pip packages:

```bash
pip list
```

Show package information:

```bash
pip show <package>
```

---

# 17. Save Project Dependencies

Export the Conda environment:

```bash
conda env export > environment.yml
```

Recreate it:

```bash
conda env create -f environment.yml
```

Export pip packages:

```bash
pip freeze > requirements.txt
```

Install from requirements:

```bash
pip install -r requirements.txt
```

### Recommended

For a project repository, keep:

```text
project/
├── README.md
├── requirements.txt
└── environment.yml
```

Use `requirements.txt` for Python/PyPI dependencies and `environment.yml` when you want to reproduce the Conda environment itself.

---

# 18. Recommended `.gitignore`

For Python/ML projects:

```gitignore
# Python
__pycache__/
*.py[cod]
*.pyo

# Virtual environments
.venv/
venv/
env/

# Jupyter
.ipynb_checkpoints/

# Environment variables
.env
.env.local

# IDE
.vscode/
.idea/

# Python cache
.pytest_cache/
.mypy_cache/

# ML artifacts
*.pt
*.pth
*.ckpt
*.onnx

# Large datasets
data/
datasets/

# Logs
*.log

# OS
.DS_Store
Thumbs.db
```

---

# 19. Disk Space Management

If package installation produces:

```text
OSError: [Errno 122] Disk quota exceeded
```

check available disk space:

```bash
df -h
```

Check the Miniconda directory:

```bash
du -sh ~/miniconda3
```

Check Conda cache:

```bash
du -sh ~/miniconda3/pkgs
```

Clean Conda cache:

```bash
conda clean --all
```

Remove unused environments:

```bash
conda env list
```

Then:

```bash
conda remove -n <environment-name> --all
```

Check pip cache:

```bash
pip cache dir
```

Clear pip cache:

```bash
pip cache purge
```

---

# 20. Fix Common Jupyter Problems

If the `py312` kernel does not appear:

```bash
python -m ipykernel install \
--user \
--name py312 \
--display-name "Python 3.12 (py312)"
```

Check:

```bash
jupyter kernelspec list
```

If Jupyter is using the wrong Python:

```bash
which python
```

Then:

```bash
python -c "import sys; print(sys.executable)"
```

Make sure the path contains:

```text
envs/py312/
```

---

# 21. Fix Wrong Python Version

Check:

```bash
python --version
```

If it shows Python 3.14 instead of Python 3.12:

```bash
conda activate py312
```

Then:

```bash
python --version
```

Also check:

```bash
which python
```

Do not install project dependencies into the system Python.

---

# 22. Update the Environment

Update Conda:

```bash
conda update -n base -c defaults conda
```

Update Conda packages:

```bash
conda update --all
```

Update pip:

```bash
python -m pip install --upgrade pip
```

Update a specific package:

```bash
pip install --upgrade <package>
```

---

# 23. Recreate the Environment

If the environment becomes corrupted:

```bash
conda deactivate
```

Remove it:

```bash
conda remove -n py312 --all
```

Create it again:

```bash
conda create -n py312 python=3.12 -y
```

Activate:

```bash
conda activate py312
```

Upgrade pip:

```bash
python -m pip install --upgrade pip
```

Install dependencies:

```bash
pip install -r requirements.txt
```

Register Jupyter:

```bash
python -m ipykernel install \
--user \
--name py312 \
--display-name "Python 3.12 (py312)"
```

---

# 24. Recommended ML Project Workflow

Create the environment:

```bash
conda create -n py312 python=3.12 -y
```

Activate:

```bash
conda activate py312
```

Upgrade pip:

```bash
python -m pip install --upgrade pip
```

Install dependencies:

```bash
pip install -r requirements.txt
```

Register Jupyter:

```bash
python -m ipykernel install \
--user \
--name py312 \
--display-name "Python 3.12 (py312)"
```

Verify:

```bash
python --version
```

Then:

```bash
python -c "import torch; print(torch.__version__)"
```

Finally:

```bash
jupyter lab
```

---

# 25. Quick Setup

For a completely new machine, the essential commands are:

```bash
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh

bash Miniconda3-latest-Linux-x86_64.sh

source ~/.bashrc

conda create -n py312 python=3.12 -y

conda activate py312

python -m pip install --upgrade pip

pip install -r requirements.txt

python -m ipykernel install \
--user \
--name py312 \
--display-name "Python 3.12 (py312)"
```

Verify:

```bash
python --version

which python

python -c "import torch; print(torch.__version__)"

python -c "import torch; print('CUDA:', torch.cuda.is_available())"
```

---

# 26. Daily Usage

Every time you start working:

```bash
conda activate py312
```

Go to your project:

```bash
cd /path/to/project
```

Open VS Code:

```bash
code .
```

Run Python:

```bash
python main.py
```

Start Jupyter:

```bash
jupyter lab
```

When finished:

```bash
conda deactivate
```

---

# 27. Final Environment

```text
Miniconda
   │
   └── py312
        │
        ├── Python 3.12
        │
        ├── NumPy
        ├── SciPy
        ├── Pandas
        ├── Matplotlib
        ├── Seaborn
        ├── Scikit-learn
        ├── XGBoost
        │
        ├── PyTorch
        ├── TorchVision
        ├── TorchAudio
        │
        ├── Transformers
        ├── Datasets
        ├── Accelerate
        │
        ├── OpenCV
        ├── Pillow
        │
        ├── Jupyter
        ├── JupyterLab
        └── IPyKernel
```

---

# 28. Important Notes

* Use **Python 3.12** for this environment.
* Always activate `py312` before installing project packages.
* Avoid installing ML dependencies into system Python.
* Use a separate Conda environment for projects with conflicting dependencies.
* Keep `requirements.txt` inside each project.
* Use `environment.yml` when complete Conda environment reproduction is required.
* Check `torch.cuda.is_available()` before assuming PyTorch is using the GPU.
* The CUDA version shown by `nvidia-smi` and the CUDA runtime used by PyTorch are not necessarily the same.
* Avoid unnecessarily installing multiple versions of the same package.
* Keep large datasets and model checkpoints outside Git repositories unless using Git LFS or another artifact-storage solution.

---

# 29. Minimal Command Reference

```bash
# Activate
conda activate py312

# Deactivate
conda deactivate

# Python version
python --version

# Python location
which python

# Installed packages
pip list

# Conda packages
conda list

# Install dependencies
pip install -r requirements.txt

# Save pip dependencies
pip freeze > requirements.txt

# Export Conda environment
conda env export > environment.yml

# Start Jupyter
jupyter lab

# Check GPU
nvidia-smi

# Check PyTorch CUDA
python -c "import torch; print(torch.cuda.is_available())"

# Check GPU from PyTorch
python -c "import torch; print(torch.cuda.get_device_name(0) if torch.cuda.is_available() else 'CUDA unavailable')"

# Clean Conda cache
conda clean --all

# Clean pip cache
pip cache purge
```

---

## Environment Summary

```text
Environment : py312
Python      : 3.12
Platform    : Ubuntu Linux
Purpose     : Data Science / ML / DL / LLM
IDE         : VS Code
Notebook    : Jupyter / JupyterLab
GPU         : NVIDIA RTX 2050 4 GB
```
