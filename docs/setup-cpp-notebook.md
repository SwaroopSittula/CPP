# Setting Up Jupyter Notebook with C++ Kernel

This guide provides step-by-step instructions to set up a Jupyter Notebook environment for running C++ code using the
`xeus-cling` kernel.

## Prerequisites

- Ubuntu 20.04+ (or any Linux distribution)
- Python 3 installed
- VS Code (optional but recommended)

## Step 1: Install Conda (Miniconda Recommended)

Conda is required to install `xeus-cling`.z Install Miniconda with the following commands:

```sh
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
bash Miniconda3-latest-Linux-x86_64.sh
```

Follow the prompts and restart your shell:

```sh
source ~/.bashrc
```

Verify installation:

```sh
conda --version
```

### (Optional) Install Mamba for Faster Package Management

Mamba is a faster alternative to Conda:

```sh
conda install -c conda-forge mamba
```

Now, you can use mamba instead of conda for faster package installation.

## Step 2: Install Jupyter Notebook

Install Jupyter Notebook using Conda:

```sh
conda install -c conda-forge notebook
```

## Step 3: Install `xeus-cling` (C++ Kernel)

Now install the `xeus-cling` kernel to run C++ code in Jupyter:

```sh
conda install -c conda-forge xeus-cling
```

## Step 4: Register the Kernel

If `xeus-cling` is not listed, manually install it:

```sh
# Ensure Conda is initialized:
conda init
source ~/.bashrc

# Ensure the kernel is correctly
jupyter kernelspec list

# Get conda base path
conda info --base

# Check the kernels installed in conda base path
ls $(conda info --base)/share/jupyter/kernels/

# Add the kernel to jupyter kernelspec
jupyter kernelspec install --user $(conda info --base)/share/jupyter/kernels/xeus-cling

# Then verify kernelspec list again.
jupyter kernelspec list
```


## Step 5: Launch Jupyter Notebook

Start Jupyter Notebook by running:

```sh
jupyter notebook
```

Alternatively, if using VS Code, install the **Jupyter** extension and open a new Jupyter Notebook (`.ipynb`). Select
the **C++ (Cling) Kernel**.

## Step 6: Run C++ Code

Create a new Jupyter Notebook and enter the following C++ code in a cell:

```cpp
#include <iostream>
using namespace std;

cout << "Hello, C++ in Jupyter!" << endl;
```

Run the cell, and you should see the output displayed below.

## Troubleshooting

If you face issues, try the following:
`

### 1. Cannot Select Kernel in VS Code

- Restart VS Code (`Ctrl+Shift+P` → `Reload Window`).
- Open a Jupyter Notebook and check the kernel selection.
- Look for **C++ (xcpp11, xcpp14, xcpp17)** and select it.

### 2. Installation Issues

- Ensure Conda is properly installed and updated:
  ```sh
  conda update conda
  conda update --all
  ```
- If `xeus-cling` is missing:
  ```sh
  conda install -c conda-forge xeus-cling
  ```

## Conclusion

You have now successfully set up Jupyter Notebook with a C++ kernel. You can use it to write and execute C++ code
interactively within a notebook.

Happy Coding! 🚀

