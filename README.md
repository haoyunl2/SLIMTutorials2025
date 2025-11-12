# SLIMTutorial2025

**Tutorials for the 2025 ML4Seismic Meeting**

This repository explains how to access, copy, and run the ML4Seismic 2025
tutorials on the shared JupyterHub server. Each tutorial has its own Julia
`Project.toml` and `Manifest.toml` for reproducibility.

---

## 1. Getting Started (for Participants)

### A. Log in
Open your browser and visit:
```
http://<SERVER_IP>
```
Use the credentials provided by the organizers. First login will ask you to set
a password.

---

### B. Copy Tutorials to Your Home Directory
Shared (read-only) directory:
```
/opt/ml4seismic_tutorial_2025/
```
Copy to your home:
```bash
cp -r /opt/ml4seismic_tutorial_2025 ~/ml4seismic_tutorial_2025
```
Directory structure:
```
~/ml4seismic_tutorial_2025/
├── tutorial_1/
│   ├── Project.toml
│   ├── Manifest.toml
│   └── tutorial_notebook.ipynb
├── tutorial_2/
│   └── …
```
Each folder is an independent Julia environment.

---

### C. Enable the Julia Kernel in Jupyter
Open a terminal in JupyterHub and run:
```bash
julia -e 'using Pkg; Pkg.add("IJulia")'
```
Then reload → **Kernel → Change Kernel → Julia 1.11**

---

### D. Build the Tutorial Environment
Example:
```bash
cd ~/ml4seismic_tutorial_2025/tutorial_1
julia
```
In the Julia REPL:
```julia
using Pkg
Pkg.activate(".")
Pkg.instantiate()
```
To add extra packages:
```julia
Pkg.add(["Plots","SlimOptim","JutulDarcy"])
```

---

## 2. Notes
* Do not modify `/opt/ml4seismic_tutorial_2025`.
* Work only in your personal copy.
* Save often (servers may auto-restart when idle).
* If the Julia kernel disappears, rerun `Pkg.add("IJulia")` and refresh.

---

## 3. Troubleshooting

| Issue                  | Fix                                                           |
| ---------------------- | ------------------------------------------------------------- |
| Kernel not found       | Run `Pkg.add("IJulia")` again and refresh Jupyter.            |
| Permission denied      | You are editing `/opt/...` — work in your copy instead.       |
| `Pkg.instantiate()` slow | Ask admins to preinstall packages in `/opt/julia_depot`.    |
| Manifest mismatch      | Use Julia 1.11 and activate the correct environment.          |

---

## 4. Contact
* **Prof. Felix J. Herrmann** — felix.herrmann@gatech.edu
* **Haoyun Li** — hli853@gatech.edu

© 2025 SLIM Group, Georgia Tech — Infrastructure for ML4Seismic 2025
