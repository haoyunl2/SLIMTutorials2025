# SLIMTutorial2025

[![Julia](https://img.shields.io/badge/Julia-1.11.x-9558B2.svg?style=flat&logo=julia)](https://julialang.org)
[![JupyterHub](https://img.shields.io/badge/JupyterHub-Server-brightgreen?style=flat&logo=jupyter)]()
[![Reproducible](https://img.shields.io/badge/Reproducible-Environments-blue.svg)]()
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)]()

**Tutorials for the 2025 ML4Seismic Meeting**

This repository explains how to access, copy, and run all ML4Seismic 2025 tutorials on the shared JupyterHub server.  
Each tutorial comes with its own `Project.toml` and `Manifest.toml`, ensuring **fully reproducible Julia environments**.

---

## Table of Contents

- [1. Accessing JupyterHub](#1-accessing-jupyterhub)
- [2. Copying Tutorials](#2-copying-tutorials)
- [3. Julia Kernel Setup](#3-julia-kernel-setup)
- [4. Running a Tutorial](#4-running-a-tutorial)
- [5. Notes for Participants](#5-notes-for-participants)
- [6. Troubleshooting](#6-troubleshooting)
- [7. Directory Layout](#7-directory-layout)
- [8. Contact](#8-contact)

---

## 1. Accessing JupyterHub

Open your browser and visit:

```
http://128.85.36.226/
```

Use the username/password provided by the organizers.  
Your first login will prompt you to set a new password.

---

## 2. Copying Tutorials

All tutorials are stored in a **read-only shared directory**:

```
/opt/ml4seismic_tutorial_2025/
```

Make your own copy:

```bash
cp -r /opt/ml4seismic_tutorial_2025 ~/ml4seismic_tutorial_2025
```

Work **only** inside your personal copy.

---

## 3. Julia Kernel Setup

If the Julia kernel is not available in Jupyter:

```bash
julia -e 'using Pkg; Pkg.add("IJulia")'
```

Then refresh JupyterHub and select:

**Kernel → Change Kernel → Julia 1.11**

---

## 4. Running a Tutorial

### 4.1 Activate the Environment

In the JupyterHub terminal:

```bash
cd ~/ml4seismic_tutorial_2025/tutorial_1
julia
```

Inside the Julia REPL:

```julia
using Pkg
Pkg.activate(".")
Pkg.instantiate()
```

### 4.2 Install Optional Packages (if needed)

```julia
Pkg.add(["Plots", "SlimOptim", "JutulDarcy"])
```

---

## 5. Notes for Participants

- The directory `/opt/ml4seismic_tutorial_2025/` is **read-only**.
- Save your work frequently; the JupyterHub server may restart after idle.
- Always activate the correct environment before running any notebook.
- All tutorials require **Julia 1.11.x**.
- If using GPU-enabled examples, ensure you select a GPU runtime (if available).

---

## 6. Troubleshooting

| Issue                           | Solution |
|--------------------------------|----------|
| Julia kernel missing           | Install IJulia and refresh JupyterHub |
| Permission denied              | You attempted to edit `/opt/...` → switch to `~/ml4seismic_tutorial_2025` |
| Slow `Pkg.instantiate()`       | Ask admins to preinstall packages in `/opt/julia_depot/` |
| Manifest warnings / mismatch   | Ensure Julia 1.11 and activate correct tutorial folder |
| Kernel won’t start             | Restart Jupyter server (Control Panel → Stop → Start) |

---

## 7. Directory Layout

```
~/ml4seismic_tutorial_2025/
├── tutorial_1/
│   ├── Project.toml
│   ├── Manifest.toml
│   └── tutorial_notebook.ipynb
├── tutorial_2/
│   ├── Project.toml
│   ├── Manifest.toml
│   └── ...
└── tutorial_N/
```

Each folder is its own Julia environment with pinned versions.

---

## 8. Contact

**Prof. Felix J. Herrmann**  
felix.herrmann@gatech.edu  

**Haoyun Li**  
hli853@gatech.edu  

© 2025 SLIM Group, Georgia Tech — Infrastructure for ML4Seismic 2025
