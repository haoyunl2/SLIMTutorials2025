# **ML4Seismic 2025**

```markdown
# SLIMTutorials2025

[![Python](https://img.shields.io/badge/Python-3.12+-3776AB.svg?style=flat&logo=python)](https://www.python.org/)
[![Julia](https://img.shields.io/badge/Julia-1.11+-9558B2.svg?style=flat&logo=julia)](https://julialang.org/)
[![JupyterHub](https://img.shields.io/badge/JupyterHub-Server-brightgreen?style=flat&logo=jupyter)]()
[![Reproducible](https://img.shields.io/badge/Reproducible-Environments-blue.svg)]()
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)]()

**Tutorials for the ML4Seismic Meeting 2025**

This repository provides instructions for accessing, copying, and running all Python and Julia tutorials on the shared JupyterHub server.  
All tutorials are fully reproducible and isolated via local environments.

---

## Table of Contents

- [1. Accessing JupyterHub](#1-accessing-jupyterhub)
- [2. Copying Tutorials](#2-copying-tutorials)
- [3. Python Environment Setup](#3-python-environment-setup)
- [4. Julia Environment Setup](#4-julia-environment-setup)
- [5. Running Tutorials](#5-running-tutorials)
- [6. Notes for Participants](#6-notes-for-participants)
- [7. Troubleshooting](#7-troubleshooting)
- [8. Directory Layout](#8-directory-layout)
- [9. Contact](#9-contact)

---

## 1. Accessing JupyterHub

Open your browser and go to:

```

[https://slimtutorials2025.store](https://slimtutorials2025.store)

```

Log in using the credentials provided by the organizers.  
Your first login will require you to set a new password.

---

## 2. Copying Tutorials

All official tutorials are stored in a **read-only shared directory**:

```

/opt/ml4seismic_tutorial_2025/

````

Make your own editable copy:

```bash
cp -r /opt/ml4seismic_tutorial_2025 ~/ml4seismic_tutorial_2025
````

Work **only** inside your personal copy.

---

# 3. Python Environment Setup

Each Python tutorial has its own `requirements.txt`.
You may use the automated or manual method.

---

## 3.1 Automated Setup (Recommended)

Many tutorials include a `setup.sh`:

```bash
cd ~/ml4seismic_tutorial_2025/tutorial_1
chmod +x setup.sh
./setup.sh
```

This script will:

* Create a virtual environment (`.venv`)
* Install dependencies from `requirements.txt`
* Register a Jupyter kernel

---

## 3.2 Manual Setup

### Option A: pip (Standard)

```bash
cd ~/ml4seismic_tutorial_2025/tutorial_1
python3 -m venv .venv
source .venv/bin/activate
pip install --upgrade pip
pip install -r requirements.txt
```

### Option B: uv (Faster)

```bash
cd ~/ml4seismic_tutorial_2025/tutorial_1
uv venv
source .venv/bin/activate
uv pip install -r requirements.txt
```

---

## 3.3 Register a Jupyter Kernel

After activating your `.venv`:

```bash
pip install ipykernel
python -m ipykernel install --user --name tutorial_1 --display-name "Python (tutorial_1)"
```

Then select:

**Kernel → Change Kernel → Python (tutorial_1)**

---

# 4. Julia Environment Setup

The JupyterHub is already configured with a **shared Julia package depot**:

```
/opt/julia_depot
```

This depot contains all official packages (Jutul, JutulDarcy, GeoEnergyIO, GLMakie, etc.) preinstalled by the admins.
Users **do not need to install these packages**.

Each user also has a private Julia depot:

```
$HOME/.julia
```

The system automatically uses:

```
JULIA_DEPOT_PATH=/opt/julia_depot:$HOME/.julia
```

This means:

* Official packages load instantly from `/opt/julia_depot` (read-only)
* Any additional packages you install go to your personal `$HOME/.julia`

---

## 4.1 Using the Official Julia Tutorial Environment

Each Julia tutorial includes a `Project.toml`.

In the first cell of the notebook:

```julia
using Pkg
Pkg.activate(".")      # activate the tutorial environment
Pkg.instantiate()      # installs missing packages into ~/.julia
```

Then simply load packages:

```julia
using Jutul, JutulDarcy, GeoEnergyIO, GLMakie
using DataFrames, CSV, JLD2, PyPlot
```

Because the shared depot already includes these packages, this step is fast and does **not** write to system directories.

---

## 4.2 For Contributors with Custom Environments

If you have your own repository with its own `Project.toml`:

```julia
using Pkg
Pkg.activate("/home/<username>/myproject")
Pkg.instantiate()    # installs only your project's missing packages
```

Anything you install via:

```julia
Pkg.add("Flux")
Pkg.add("CUDA")
```

will be written to:

```
$HOME/.julia
```

and will NOT affect other users or the system.

---

# 5. Running Tutorials

### Python

1. Activate virtual environment:

   ```bash
   source .venv/bin/activate
   ```
2. Start notebook or select the correct kernel.

### Julia

1. In the notebook:

   ```julia
   using Pkg
   Pkg.activate(".")
   ```
2. Select the **Julia 1.11** kernel.

---

# 6. Notes for Participants

* Never modify files in `/opt/ml4seismic_tutorial_2025/` — it is read-only.
* Use a personal copy under your home directory.
* Python: each tutorial has its own `.venv`.
* Julia: use `Pkg.activate(".")` inside each tutorial directory.
* DO NOT run `Pkg.add` on the system depot — everything you need is already installed.
* Additional packages you install go to your private depot (`~/.julia`).

---

# 7. Troubleshooting

| Issue                            | Solution                                                                      |
| -------------------------------- | ----------------------------------------------------------------------------- |
| `Permission denied`              | You tried to write to `/opt/...` — switch to your local copy.                 |
| Julia package installation fails | Admin packages are read-only. Use `Pkg.activate(".")` — writes to `~/.julia`. |
| Missing Python kernel            | Re-install kernel: `python -m ipykernel install --user --name <name>`         |
| Julia doesn't see a package      | Run `Pkg.instantiate()` inside the tutorial directory.                        |
| Notebook stuck or kernel dead    | Restart your server (`Control Panel → Stop My Server`).                       |
| GPU unavailable                  | Not all VM types contain GPUs; contact organizers if required.                |

---

# 8. Directory Layout

```
/opt/ml4seismic_tutorial_2025/     # read-only official copy
~/ml4seismic_tutorial_2025/        # your editable copy
    ├── python_tutorial_1/
    │   ├── requirements.txt
    │   ├── setup.sh
    │   ├── .venv/
    │   └── notebook.ipynb
    ├── julia_tutorial_1/
    │   ├── Project.toml
    │   ├── Manifest.toml  (optional)
    │   └── notebook.ipynb
    └── ...
```

---

# 9. Contact

**Prof. Felix J. Herrmann**
[felix.herrmann@gatech.edu](mailto:felix.herrmann@gatech.edu)

**Haoyun Li**
[hli853@gatech.edu](mailto:hli853@gatech.edu)

© 2025 SLIM Group, Georgia Tech — Infrastructure for ML4Seismic 2025

````
