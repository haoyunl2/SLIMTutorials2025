# **ML4Seismic 2025 Tutorials**

[![Python](https://img.shields.io/badge/Python-3.12+-3776AB.svg?style=flat\&logo=python)](https://www.python.org/)
[![Julia](https://img.shields.io/badge/Julia-1.11+-9558B2.svg?style=flat\&logo=julia)](https://julialang.org/)
[![JupyterHub](https://img.shields.io/badge/JupyterHub-Server-brightgreen?style=flat\&logo=jupyter)]()
[![Reproducible](https://img.shields.io/badge/Reproducible-Environments-blue.svg)]()
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)]()

This repository provides instructions for accessing, copying, and running all Python and Julia tutorials on the shared JupyterHub server for **ML4Seismic 2025**.
All tutorials use fully reproducible, self-contained environments.

---

## **Table of Contents**

1. [Accessing JupyterHub](#1-accessing-jupyterhub)
2. [Copying Tutorials](#2-copying-tutorials)
3. [Python Environment Setup](#3-python-environment-setup)
4. [Julia Environment Setup](#4-julia-environment-setup)
5. [Running Tutorials](#5-running-tutorials)
6. [Notes for Participants](#6-notes-for-participants)
7. [Troubleshooting](#7-troubleshooting)
8. [Directory Layout](#8-directory-layout)
9. [Contact](#9-contact)

---

# **1. Accessing JupyterHub**

Open your browser and visit:

👉 **[https://slimtutorials2025.store](https://slimtutorials2025.store)**

Log in using the credentials provided by the organizers.
Your first login will require setting a new password.

---

# **2. Copying Tutorials**

The official read-only tutorials are located at:

```
/opt/ml4seismic_tutorial_2025/
```

Copy them into your home directory:

```bash
cp -r /opt/ml4seismic_tutorial_2025 ~/ml4seismic_tutorial_2025
```

You should **only modify your personal copy**.

---

# **3. Python Environment Setup**

Each Python tutorial has its own `requirements.txt` and optional `setup.sh`.

---

## **3.1 Automated Setup (Recommended)**

If the tutorial contains a `setup.sh`:

```bash
cd ~/ml4seismic_tutorial_2025/tutorial_1
chmod +x setup.sh
./setup.sh
```

This will:

* Create a `.venv`
* Install dependencies
* Register a Jupyter kernel

---

## **3.2 Manual Setup**

### **Option A: pip**

```bash
cd ~/ml4seismic_tutorial_2025/tutorial_1
python3 -m venv .venv
source .venv/bin/activate
pip install --upgrade pip
pip install -r requirements.txt
```

### **Option B: uv (Faster)**

```bash
cd ~/ml4seismic_tutorial_2025/tutorial_1
uv venv
source .venv/bin/activate
uv pip install -r requirements.txt
```

---

## **3.3 Registering a Jupyter Kernel**

After activating your `.venv`:

```bash
pip install ipykernel
python -m ipykernel install --user --name tutorial_1 --display-name "Python (tutorial_1)"
```

Then select:

**Kernel → Change Kernel → Python (tutorial_1)**

---

# **4. Julia Environment Setup**

The JupyterHub already defines:

```
JULIA_DEPOT_PATH=/opt/julia_depot:$HOME/.julia
```

Meaning:

* All official packages (Jutul, JutulDarcy, GeoEnergyIO…) live in **/opt/julia_depot**.
* Your personal packages go into **$HOME/.julia**.
* You do **not** need to install core packages.

---

## **4.1 Using Tutorial Environments**

Each Julia tutorial has a `Project.toml`.

Inside the notebook:

```julia
using Pkg
Pkg.activate(".")
Pkg.instantiate()
```

Then simply:

```julia
using Jutul, JutulDarcy, GeoEnergyIO, GLMakie
using DataFrames, CSV, JLD2, PyPlot
```

Since everything is preinstalled in `/opt/julia_depot`, this is fast.

---

## **4.2 For Contributors (Custom Projects)**

```julia
using Pkg
Pkg.activate("/home/<username>/myproject")
Pkg.instantiate()
```

Custom packages installed via:

```julia
Pkg.add("Flux")
Pkg.add("CUDA")
```

will be stored under:

```
~/.julia
```

and will not affect other users.

---

# **5. Running Tutorials**

## **Python**

1. Activate the environment:

   ```bash
   source .venv/bin/activate
   ```
2. Select kernel **Python (tutorial_1)**.

---

## **Julia**

```julia
using Pkg
Pkg.activate(".")
```

Then choose the **Julia 1.11** kernel.

---

# **6. Notes for Participants**

* Do **not** modify anything in `/opt/ml4seismic_tutorial_2025/`.
* Always work inside `~/ml4seismic_tutorial_2025`.
* Python tutorials each use **separate virtual environments**.
* Julia uses **Pkg.activate(".")** inside each tutorial.
* Avoid `Pkg.add` in system depot — everything required is installed.
* Personal package installs go to `~/.julia` and are safe.

---

# **7. Troubleshooting**

| Issue                          | Solution                                                                   |
| ------------------------------ | -------------------------------------------------------------------------- |
| `Permission denied`            | You attempted to modify `/opt/...`. Use your personal copy.                |
| Julia installation errors      | You tried to write to the shared depot; activate local project first.      |
| Python kernel missing          | Reinstall kernel using `python -m ipykernel install --user --name <name>`. |
| Missing Julia packages         | Run `Pkg.instantiate()` inside the tutorial directory.                     |
| Notebook crashes / dead kernel | Control Panel → **Stop My Server** → Restart.                              |
| GPU not visible                | The VM may not support GPUs — contact organizers.                          |

---

# **8. Directory Layout**

```
/opt/ml4seismic_tutorial_2025/      # Official, read-only
~/ml4seismic_tutorial_2025/         # User’s working copy
    ├── python_tutorial_1/
    │   ├── requirements.txt
    │   ├── setup.sh
    │   ├── .venv/
    │   └── notebook.ipynb
    ├── julia_tutorial_1/
    │   ├── Project.toml
    │   ├── Manifest.toml
    │   └── notebook.ipynb
    └── ...
```

---

# **9. Contact**

**Prof. Felix J. Herrmann**
📧 [felix.herrmann@gatech.edu](mailto:felix.herrmann@gatech.edu)

**Haoyun Li**
📧 [hli853@gatech.edu](mailto:hli853@gatech.edu)

© 2025 SLIM Group, Georgia Tech — Infrastructure for ML4Seismic 2025
