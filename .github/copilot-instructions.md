# Data Library - Project Setup Guide

## Overview

A step-by-step Copilot guide to set up a [Data Library for Python](https://developers.lseg.com/en/api-catalog/lseg-data-platform/lseg-data-library-for-python) development environment with Python and JupyterLab on Windows and macOS.

## Prerequisites

- Python 3.11 or higher installed and available on your `PATH`
- Git installed and configured
- Network access to PyPI (or a trusted mirror)

## Working Directory (Important)

Run all commands in this guide from the **workspace root** folder.

## Expected Project Layout

Before running setup commands, confirm the project structure should match this layout:

```text
/
├── .github/
│   └── copilot-instructions.md
├── .vscode/
│   └── settings.json
├── .gitignore
├── LICENSE.md
├── Project_README.md
├── README.md (for the repository)
├── images/
├── requirements.txt
├── .venv/
└── notebook/
    ├── ld_notebook.ipynb
    └── lseg-data.config.json
```

Notes:
- `.venv/` must be inside the workspace root.
- `notebook/` must contain both `ld_notebook.ipynb` and `lseg-data.config.json`.

---

## Part 1: Create a Project Setup Branch

1. Verify that the current branch is `main`:

   ```bash
   git branch --show-current
   ```

   If the command does not return `main`, switch to `main` before continuing.

2. Check out a new git branch named `setup-project`:

   ```bash
   git checkout -b setup-project
   ```

3. Add a `Project_README.md` with `# Data Library Jupyter Notebook` title.

4. Add a `.gitignore` file suitable for Python projects (e.g., from [gitignore.io](https://www.toptal.com/developers/gitignore/api/python)).

5. Add the `.venv/` virtual environment folder to `.gitignore`.

---

## Part 2: Set Up the Python Virtual Environment

> **Prerequisite:** The Part 1 must be completed and the git branch must be on `setup-project` branch before proceeding with these steps.

1. Create a virtual environment named `.venv` inside the workspace root:

   ```bash
   python -m venv .venv
   ```

   This must create `.venv` at the workspace root.

2. Activate the environment:

   - **Windows (PowerShell):**
     ```powershell
     .\.venv\Scripts\Activate.ps1
     ```
   - **Windows (CMD):**
     ```cmd
     .venv\Scripts\activate.bat
     ```
   - **macOS / Linux:**
     ```bash
     source .venv/bin/activate
     ```

3. Update pip to the latest version:

   - **Windows (PowerShell/CMD):**
     ```powershell
     python -m pip install --trusted-host pypi.python.org --trusted-host files.pythonhosted.org --trusted-host pypi.org --no-cache-dir --upgrade pip
     ```
   - **macOS:**
     ```bash
     python3 -m pip install --trusted-host pypi.python.org --trusted-host files.pythonhosted.org --trusted-host pypi.org --no-cache-dir --upgrade pip
     ```

4. Install the required packages:

   - **Windows (PowerShell/CMD):**
     ```powershell
     python -m pip install --trusted-host pypi.python.org --trusted-host files.pythonhosted.org --trusted-host pypi.org --no-cache-dir lseg-data jupyterlab
     ```
   - **macOS:**
     ```bash
     python3 -m pip install --trusted-host pypi.python.org --trusted-host files.pythonhosted.org --trusted-host pypi.org --no-cache-dir lseg-data jupyterlab
     ```

5. Save the installed dependencies to `requirements.txt`:

   - **Windows (PowerShell/CMD):**
     ```powershell
     python -m pip freeze > requirements.txt
     ```
   - **macOS:**
     ```bash
     python3 -m pip freeze > requirements.txt
     ```

6. Create `.vscode/settings.json` with the following content:

   ```json
   {
     "git.ignoreLimitWarning": true
   }
   ```

7. Create the following file and folder structure under the project root:

   ```
   notebook/
   ├── ld_notebook.ipynb
   └── lseg-data.config.json
   ```

8. Create `lseg-data.config.json` inside `notebook` with the following content:

   ```json
   {
     "logs": {
       "level": "debug",
       "transports": {
         "console": {
           "enabled": false
         },
         "file": {
           "enabled": false,
           "name": "lseg-data-lib.log"
         }
       }
     }
   }
   ```

---

## Part 3: Notebook Code

Open `notebook/ld_notebook.ipynb` in JupyterLab and run the following cells in order.

1. **Import the library:**

   ```python
   import lseg.data as ld
   ```

2. **Open a session (connects to LSEG Workspace):**

   ```python
   ld.open_session()
   ```

3. **Retrieve market data** (BID/ASK for EUR and JPY):

   ```python
   ld.get_data(universe = ['/EUR=','/JPY='], fields = ['BID','ASK'])
   ```

4. Do not need to run the notebook cells. Developers can run them by themselves to verify the setup is working. 

---

## Part 4: Finish a Project Setup Branch

> **Prerequisite:** The Part 3 must be completed and the notebook should have outputs saved back into `ld_notebook.ipynb` before proceeding with these steps.

1. Ensure that the git branch is `setup-project`:

   ```bash
   git branch --show-current
   ```

   If the command does not return `setup-project`, switch to `setup-project` before continuing.

2. Review the changes in the `setup-project` branch to confirm that all expected files are created and updated:

   ```bash
   git status
   git diff
   ```  

3. Stage all files and create a commit on `setup-project`:

   ```bash
   git add .
   git commit -m "setup: initial project structure with notebook and dependencies"
   ```
