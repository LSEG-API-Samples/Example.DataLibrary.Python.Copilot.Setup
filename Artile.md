# Automated LSEG Data Library Jupyter Notebook Setup with GitHub Copilot

- Version: 1.0
- Last update: May 2026
- Environment: Python + Git + Copilot

## Copilot .github/copilot-instructions.md Walkthrough

This project `.github/copilot-instructions.md` file is a [Markdown](https://www.markdownguide.org/) text file contains the project overview, prerequisites, expected project structure information, and a step-by-step guide to set up a Python and [Jupyterlab](https://jupyter.org/) development environment for [LSEG Data Library for Python](https://developers.lseg.com/en/api-catalog/lseg-data-platform/lseg-data-library-for-python) (aka Data Library version 2).

I am explaining the file part-by-part, so it should be easy for developers to follows and understand each part purpose and actions.

### Overview and Prerequisites

Let me start by the first section, overview and prerequisites. This section describes the project's overview (you can change it based on your project requirements) and prerequisites. The basic prerequisites are Python, [Git client application](https://git-scm.com/), and access to [PyPI](https://pypi.org/) Python Package Index repository.

**Note**: The Python, Pip tool, and Git client must be installed and configured on your OS `PATH`

```markdown
# Data Library - Project Setup Guide

## Overview

A step-by-step Copilot guide to set up a [Data Library for Python](https://developers.lseg.com/en/api-catalog/lseg-data-platform/lseg-data-library-for-python) development environment with Python and JupyterLab on Windows and macOS.

## Prerequisites

- Python 3.11 or higher installed and available on your `PATH`
- Git installed and configured
- Network access to PyPI (or a trusted mirror)
```

### Working Directory and Project Layout 

My next points are the project working directory and layout. These two sections may look simple, but they are actually critical for Copilot to work correctly.

The **Working Directory** section tells Copilot and developers who running the setup — that all commands must be executed from the **workspace root** folder. Without this, Copilot/Developers might create files or virtual environments in the wrong location, which would cause the rest of the setup steps to fail.

```markdown
## Working Directory (Important)

Run all commands in this guide from the **workspace root** folder.
```

The **Expected Project Layout** section defines the full folder and file structure that the project should have after setup is complete. This gives Copilot a clear target to work toward. Instead of guessing where to create files, Copilot can refer to this layout and place every file exactly where it belongs.

````markdown
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
````

The notes at the bottom are especially useful. They highlight the parts of the layout that are easy to get wrong — for example, `.venv/` must be at the workspace root, not inside a subfolder, and the `notebook/` folder must contain both the notebook file and the configuration file together.

Together, these two sections anchor the entire setup. They tell Copilot where it is starting from and what the finished result should look like. 

That’s all I have to say about the project structure.

### Part 1: Set Up the Python Virtual Environment

Now we come to the first step of every Python project — setting up a Python virtual environment. A virtual environment keeps the project's dependencies isolated from your system Python, so installing or upgrading packages here will not affect other projects on your machine.

This guide demonstrates with the built-in [venv](https://docs.python.org/3/library/venv.html) module, but you can adapt the instructions in `.github/copilot-instructions.md` to use [Anaconda](https://www.anaconda.com/)/[Miniconda](https://www.anaconda.com/docs/getting-started/miniconda/main), [virtualenv](https://virtualenv.pypa.io/en/latest/), [Pipenv](https://pipenv.pypa.io/en/latest/), or [Poetry](https://python-poetry.org/) depending on your team's preference.

Once the virtual environment is created and activated, the remaining steps in this part cover: upgrading `pip` to the latest version, installing the [LSEG Data Library for Python](https://pypi.org/project/lseg-data/) and [JupyterLab](https://pypi.org/project/jupyterlab/), saving the installed dependencies list and versions to `requirements.txt`, creating a [VS Code settings](https://code.visualstudio.com/docs/configure/settings) file, and finally creating the notebook file alongside its library configuration file.


````markdown
## Part 1: Set Up the Python Virtual Environment

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
````

You may notice that I intentionally write each instruction with the exact command to run — `python -m venv .venv`, `python -m pip freeze > requirements.txt`, and so on. This level of detail is deliberate. When Copilot has a precise command to follow, it can execute the step reliably and produce a consistent result every time.

I learned this the hard way. Early on, I tried writing the instructions in a much shorter form, like this:

```txt
1. Create a Python venv name .venv
2. Activate .venv
3. Update pip
4. Install lseg-data and jupyterlab 
```

The results were unreliable. Copilot would sometimes interpret the steps differently, create the virtual environment in the wrong location, use incorrect command syntax for the operating system, or skip steps entirely. The environment it produced was inconsistent and sometimes did not work at all.

After asking Copilot to review the instructions and suggest improvements, the feedback was clear: vague, high-level steps are not enough. Copilot needs each step to include the exact command to run, the expected output or file location, and any platform-specific variations. The more detail you provide, the more reliably Copilot can follow and reproduce the setup across different machines and environments.

This is the key lesson when writing a `copilot-instructions.md` file — treat it less like a quick checklist and more like a precise runbook where nothing is left to interpretation.

[TBD]