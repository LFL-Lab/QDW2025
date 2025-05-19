# Quantum Device Design Workshop 2025: Superconducting Qubits

A repository for LF Lab's workshop materials for the [QDW](https://qdw-ucla.squarespace.com/) 2025 workshop at UCLA.

## Table of Contents

- [Software Requirements](#software-requirements)
- [Installation Instructions](#installation-instructions)
  - [Python Runtime](#python-runtime)
  - [Python Packages](#python-packages)
  - [AWS Palace](#aws-palace)
- [Materials for the Workshop](#materials-for-the-workshop)
  - [Beginner Track](#beginner-track)
  - [Advanced Track](#advanced-track)
- [Contact](#contact)

## Software Requirements

For the hands-on sessions, you will need:

1. Python runtime (Python 3.10 recommended but not required) with the following packages:
   - [`qiskit-metal`](https://github.com/qiskit-community/qiskit-metal)
   - [`SQuADDS`](https://github.com/LFL-Lab/SQuADDS)
   - [`SQDMetal`](https://github.com/SQDLab/SQDMetal)
2. [AWS Palace](https://github.com/awslabs/palace)

### Installation Instructions

> **Note for Experienced Users**: The following installation instructions are provided in great detail to help new users set up their environment from scratch. If you already have Python installed and are familiar with package management, you can skip the Python installation steps and proceed directly to installing the required packages. The detailed instructions are meant to be comprehensive for beginners while remaining flexible for experienced users to adapt to their existing setup.

| Component       | Status   | Installation Guide                    |
| --------------- | -------- | ------------------------------------- |
| Python Runtime  | Required | [View Instructions](#python-runtime)  |
| Python Packages | Required | [View Instructions](#python-packages) |
| AWS Palace      | Required | [View Instructions](#aws-palace)      |

### Python Runtime

<details>
<summary><strong>macOS Installation</strong></summary>

1. Python Installation:

   - Open Terminal:

     - Press `Command (⌘) + Space` to open Spotlight
     - Type "Terminal" and press Enter

   - Install Homebrew if you haven't already:

     ```bash
     /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
     ```

     - Follow any on-screen instructions
     - Verify Homebrew installation:
       ```bash
       brew --version
       ```

   - Install Python 3.10:

     ```bash
     brew install python@3.10
     ```

     - Wait for the installation to complete
     - Verify Python installation:
       ```bash
       python3.10 --version
       ```

   - Add Python to your PATH:
     `bash
echo 'export PATH="/usr/local/opt/python@3.10/bin:$PATH"' >> ~/.zshrc
source ~/.zshrc
` - Verify PATH is set correctly:
     `bash
  which python3.10
  `
     </details>

<details>
<summary><strong>Windows Installation</strong></summary>

1. Python Installation:

   - Download Anaconda:

     - Open your web browser and go to [Anaconda's official website](https://www.anaconda.com/products/distribution)
     - Click the "Download" button for Windows
     - Choose the 64-bit version

   - Install Anaconda:

     - Double-click the downloaded installer
     - Click "Next" through the welcome screen
     - Accept the license agreement
     - Choose "Just Me" for installation type
     - **Important**: Select the installation location (default is fine)
     - **Important**: Check both boxes:
       - "Add Anaconda to my PATH environment variable"
       - "Register Anaconda as my default Python"
     - Click "Install" and wait for completion
     - Click "Finish"

   - Open Anaconda Prompt:

     - Click the Windows Start button
     - Type "Anaconda Prompt"
     - Click on "Anaconda Prompt (anaconda3)"

   - Create and activate environment:
     `bash
conda create -n qdws python=3.10
` - When prompted, type 'y' and press Enter - After creation, activate the environment:
     `bash
  conda activate qdws
  ` - Verify the installation:
     `bash
  python --version
  `
     </details>

<details>
<summary><strong>Linux Installation</strong></summary>

1. Python Installation:

   - Open Terminal:

     - Press `Ctrl + Alt + T`
     - Or search for "Terminal" in your applications menu

   - Update package list:

     ```bash
     sudo apt update
     ```

     - Enter your password when prompted
     - Wait for the update to complete

   - Install Python 3.10 and pip:

     ```bash
     sudo apt install python3.10 python3.10-venv python3-pip
     ```

     - When prompted, type 'y' and press Enter
     - Wait for installation to complete
     - Verify Python installation:
       ```bash
       python3.10 --version
       ```

   - Create a virtual environment:
     `bash
python3.10 -m venv qdws-env
` - Activate the environment:
     `bash
  source qdws-env/bin/activate
  ` - Verify activation (you should see (qdws-env) at the start of your prompt) - Verify pip installation:
     `bash
  pip --version
  `
     </details>

---

### Python Packages

> **Important**: Both `SQuADDS` and `SQDMetal` require `qiskit-metal` as a dependency. The installation process is divided into three parts:
>
> 1. Installing `qiskit-metal` (required)
> 2. Installing `SQuADDS` (requires `qiskit-metal`)
> 3. Installing `SQDMetal` (requires `qiskit-metal`)
>
> If you already have `qiskit-metal` installed in an environment, you can skip to step 2 and install `SQuADDS` and `SQDMetal` in that environment.
>
> **Need help?** If you encounter any installation issues or challenges, please [create an issue on our GitHub repository](https://github.com/LFL-Lab/qdw2025/issues) with details of your problem. We're here to help!

<details>
<summary><strong>macOS Package Installation</strong></summary>

1.  Open Terminal:

    - Press `Command (⌘) + Space` to open Spotlight
    - Type "Terminal" and press Enter

2.  Create a directory for the workshop:

    ```bash
    mkdir -p ~/qdws_workshop
    cd ~/qdws_workshop
    ```

3.  Set up Python environment:

    - For Apple Silicon (M1/M2) Macs:

      ```bash
      # Install Rosetta 2 if not already installed
      softwareupdate --install-rosetta

      # Create environment with x86 emulation
      CONDA_SUBDIR=osx-64 conda create -n qdws python=3.10
      conda activate qdws
      conda config --env --set subdir osx-64
      ```

    - For Intel Macs:
      ```bash
      # Create environment
      conda create -n qdws python=3.10
      conda activate qdws
      ```

4.  Install qiskit-metal and its dependencies:

    ```bash
    curl -O https://raw.githubusercontent.com/Qiskit/qiskit-metal/main/environment.yml
    conda env update -n qdws -f environment.yml
    python -m pip install --no-deps -e git+https://github.com/Qiskit/qiskit-metal.git#egg=qiskit-metal
    ```

5.  Verify qiskit-metal installation:

    ```bash
    python -c "import qiskit_metal; print('Qiskit Metal version:', qiskit_metal.__version__)"
    ```

6.  Install SQuADDS in the same environment:

    ```bash
    pip install SQuADDS
    ```

7.  Verify SQuADDS installation:

    ```bash
    python -c "import squadds; print('SQuADDS version:', squadds.__version__)"
    ```

8.  Install SQDMetal in the same environment:

    ```bash
    cd ~/qdws_workshop
    git clone https://github.com/sqdlab/SQDMetal.git
    cd SQDMetal
    pip install .
    ```

9.  Verify SQDMetal installation:

    ```bash
    python -c "import SQDMetal; print('SQDMetal installed successfully')"
    ```

10. Final verification of all packages:

    ```bash
    $ python
    >>> import qiskit_metal
    >>> import squadds
    >>> import SQDMetal
    >>> exit()
    ```

    </details>

<details>
<summary><strong>Windows Package Installation</strong></summary>

1.  Open Anaconda Prompt:

    - Click the Windows Start button
    - Type "Anaconda Prompt"
    - Click on "Anaconda Prompt (anaconda3)"

2.  Create a directory for the workshop:

    ```bash
    cd %USERPROFILE%
    mkdir qdws_workshop
    cd qdws_workshop
    ```

3.  Set up Python environment:

    ```bash
    # Create environment
    conda create -n qdws python=3.10
    conda activate qdws
    ```

4.  Install qiskit-metal and its dependencies:

    ```bash
    curl -O https://raw.githubusercontent.com/Qiskit/qiskit-metal/main/environment.yml
    conda env update -n qdws -f environment.yml
    python -m pip install --no-deps -e git+https://github.com/Qiskit/qiskit-metal.git#egg=qiskit-metal
    ```

5.  Verify qiskit-metal installation:

    ```bash
    python -c "import qiskit_metal; print('Qiskit Metal version:', qiskit_metal.__version__)"
    ```

6.  Install SQuADDS in the same environment:

    ```bash
    pip install SQuADDS
    ```

7.  Verify SQuADDS installation:

    ```bash
    python -c "import squadds; print('SQuADDS version:', squadds.__version__)"
    ```

8.  Install SQDMetal in the same environment:

    ```bash
    cd %USERPROFILE%\qdws_workshop
    git clone https://github.com/sqdlab/SQDMetal.git
    cd SQDMetal
    pip install .
    ```

9.  Verify SQDMetal installation:

    ```bash
    python -c "import SQDMetal; print('SQDMetal installed successfully')"
    ```

10. Final verification of all packages:
    ```bash
    $ python
    >>> import qiskit_metal
    >>> import squadds
    >>> import sqdmetal
    >>> exit()
    ```

> **Note**: If you encounter `ERROR: Failed building wheel for klayout` while building from GitHub, install KLayout independently from [here](https://www.klayout.de/build.html) and comment out the `klayout==0.29.0` line in the `requirements.txt` file before re-running the installation commands.

</details>

<details>
<summary><strong>Linux Package Installation</strong></summary>

1.  Open Terminal:

    - Press `Ctrl + Alt + T`
    - Or search for "Terminal" in your applications menu

2.  Create a directory for the workshop:

    ```bash
    mkdir -p ~/qdws_workshop
    cd ~/qdws_workshop
    ```

3.  Set up Python environment:

    ```bash
    # Create environment
    conda create -n qdws python=3.10
    conda activate qdws
    ```

4.  Install qiskit-metal and its dependencies:

    ```bash
    curl -O https://raw.githubusercontent.com/Qiskit/qiskit-metal/main/environment.yml
    conda env update -n qdws -f environment.yml
    python -m pip install --no-deps -e git+https://github.com/Qiskit/qiskit-metal.git#egg=qiskit-metal
    ```

5.  Verify qiskit-metal installation:

    ```bash
    python -c "import qiskit_metal; print('Qiskit Metal version:', qiskit_metal.__version__)"
    ```

6.  Install SQuADDS in the same environment:

    ```bash
    pip install SQuADDS
    ```

7.  Verify SQuADDS installation:

    ```bash
    python -c "import squadds; print('SQuADDS version:', squadds.__version__)"
    ```

8.  Install SQDMetal in the same environment:

    ```bash
    cd ~/qdws_workshop
    git clone https://github.com/sqdlab/SQDMetal.git
    cd SQDMetal
    pip install .
    ```

9.  Verify SQDMetal installation:

    ```bash
    python -c "import sqdmetal; print('SQDMetal installed successfully')"
    ```

10. Final verification of all packages:
    ```bash
    $ python
    >>> import qiskit_metal
    >>> import squadds
    >>> import sqdmetal
    >>> exit()
    ```

> **Troubleshooting**: If you encounter any issues with the `datasets` library, you may need to downgrade to version 2.19.2:
>
> ```bash
> pip install datasets==2.19.2
> ```

</details>

---

### AWS Palace

> **Important**: Please keep track of where the Palace executable is installed on your system, as you will need this path later to run simulations.

<details>
<summary><strong>macOS Installation</strong></summary>

For detailed installation instructions for Palace on macOS, please refer to the [SQuADDS documentation](https://lfl-lab.github.io/SQuADDS/source/resources/palace.html#installation-of-palace-on-mac-os).

The installation process involves:

1. Installing prerequisites (Homebrew, Xcode Command Line Tools)
2. Installing dependencies (cmake, gcc, open-mpi, openblas, git)
3. Building Palace from source
4. Verifying the installation

After installation, the Palace executable will be located in the `bin/` directory of your build folder. Make note of this location for future use.

</details>

<details>
<summary><strong>Windows Installation</strong></summary>

For Windows users, we recommend using the prebuilt Palace executable provided by WELSIM. Detailed instructions can be found in the [SQuADDS documentation](https://lfl-lab.github.io/SQuADDS/source/resources/palace.html#installation-of-palace-on-windows-systems).

The prebuilt executable will be installed in:

```
C:\Program Files\WELSIM\v3.1\palace.exe
```

If you prefer to build from source, the documentation also includes detailed steps for building Palace on Windows, though this is not recommended for beginners.

</details>

<details>
<summary><strong>Linux Installation</strong></summary>

For detailed installation instructions for Palace on Linux, please refer to the [SQuADDS documentation](https://lfl-lab.github.io/SQuADDS/source/resources/palace.html#installation-of-palace-on-linux-pcs).

The installation process involves:

1. Installing system dependencies
2. Setting up Spack package manager
3. Installing MPI via Spack
4. Building Palace from source

After installation, the Palace executable will be in your build directory. Make note of this location for future use.

</details>

<details>
<summary><strong>HPC Systems Installation</strong></summary>

For HPC systems, please follow the instructions from the [official Palace site](https://awslabs.github.io/palace/stable/install/).

Additionally, [sqdlab/SQDMetal](https://github.com/sqdlab/SQDMetal) provides helpful resources for installation on HPC systems.

</details>

> **Optional**: To visualize simulation outputs, you may want to install [ParaView](https://www.paraview.org/download/). This is an optional step and not required for the workshop, but it can be helpful for visualizing the results of your simulations.

---

## Materials for the Workshop:

### Kickoff:

**Slides:** [Kickoff](presentations/Eli/kickoff.pptx)

### Beginner Track:

**Notebook:** [Designing a "fab-ready" chip with `SQuADDS`](notebooks/beginner-track/tutorial-attendees.ipynb)

**Slides:** [Designing a "fab-ready" chip with `SQuADDS`](presentations/beginner-track/slides.pptx)

### Advanced Track:

#### Setup Instructions

For advanced track participants, please follow the [detailed setup instructions](notebooks/advance-track/setup_instructions.md) to configure your environment for the ML components of the workshop.

#### Shanto:

**Notebook:** [Learning the Inverse Design Map: Hamiltonian to Geometry using Machine Learning](notebooks/advance-track/tutorial-attendees.ipynb)

**Slides:** [Learning the Inverse Design Map: Hamiltonian to Geometry using Machine Learning](presentations/advance-track/slides.pptx)

#### Eli:

**Slides:** [](presentations/Eli/.)

---

## Contact:

For any questions or further information, contact [Sadman Ahmed Shanto](mailto:shanto@usc.edu).
