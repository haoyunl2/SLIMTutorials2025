# SLIMTutorial2025

**Tutorials for the 2025 ML4Seismic Meeting**

This repository describes how to access, copy, and run the ML4Seismic 2025 tutorials on the shared JupyterHub server.
Each tutorial comes with its own `Project.toml` and `Manifest.toml` to ensure full reproducibility.

---

# 1. Getting Started (for Participants)

## A. Log in to JupyterHub

Open your browser and visit:

```
http://20.120.230.58/
```

Use the credentials provided by the organizers.
On your first login, you will be asked to set a new password.

---

## B. Copy Tutorials to Your Home Directory

The shared **read-only** tutorial directory is:

```
/opt/ml4seismic_tutorial_2025/
```

Copy the entire set of tutorials to your home directory:

```bash
cp -r /opt/ml4seismic_tutorial_2025 ~/ml4seismic_tutorial_2025
```

### Directory Structure

```
~/ml4seismic_tutorial_2025/
├── tutorial_1/
│   ├── Project.toml
│   ├── Manifest.toml
│   └── tutorial_notebook.ipynb
├── tutorial_2/
│   ├── ...
└── tutorial_N/
```

Each tutorial folder is an **independent Julia environment**.

---

# 2. Julia Kernel Setup in JupyterHub

If the Julia kernel is not visible, run:

```bash
julia -e 'using Pkg; Pkg.add("IJulia")'
```

Then refresh the JupyterHub page and set:

**Kernel → Change Kernel → Julia 1.11**

---

# 3. Running a Tutorial

## A. Activate the Tutorial Environment

Open a terminal in JupyterHub:

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

This installs all required packages for the selected tutorial.

## B. Add Optional Packages

For example:

```julia
Pkg.add(["Plots", "SlimOptim", "JutulDarcy"])
```

---

# 4. Notes for Participants

* **Do not modify** anything under `/opt/ml4seismic_tutorial_2025/`.
  Work only inside your personal copy.
* Save your work frequently—servers may restart when idle.
* Always activate the correct environment before running a tutorial.
* All tutorials require **Julia 1.11.x**.

---

# 5. Troubleshooting

| Issue                       | Fix                                                                   |
| --------------------------- | --------------------------------------------------------------------- |
| Julia kernel missing        | Run `Pkg.add("IJulia")` and refresh JupyterHub                        |
| Permission denied           | You are editing `/opt/...` — work inside `~/ml4seismic_tutorial_2025` |
| `Pkg.instantiate()` is slow | Ask admins to preinstall common packages in `/opt/julia_depot/`       |
| Manifest mismatch           | Ensure you are using **Julia 1.11** and activated the correct folder  |

---

# 6. Contact

* **Prof. Felix J. Herrmann** — [felix.herrmann@gatech.edu](mailto:felix.herrmann@gatech.edu)
* **Haoyun Li** — [hli853@gatech.edu](mailto:hli853@gatech.edu)

© 2025 SLIM Group, Georgia Tech
Infrastructure for ML4Seismic 2025

