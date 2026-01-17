# PlotNeuralNet Context

## Project Overview
**PlotNeuralNet** is a tool for creating high-quality, publication-ready visualizations of neural network architectures using **LaTeX** and **TikZ**. It provides a Python interface to define network structures, which are then compiled into LaTeX code and rendered as PDFs.

## Prerequisites
To use this project, the following must be installed:
*   **Python:** To run the generation scripts.
*   **LaTeX:** Specifically `pdflatex`.
    *   **Ubuntu:** `sudo apt-get install texlive-latex-extra` (and potentially `texlive-fonts-*` packages).
    *   **Windows:** MikTeX and a bash environment (Git Bash/Cygwin).
    *   **macOS:** MacTeX (usually includes all necessary packages).

## Key Components

### 1. Python Core (`pycore/`)
This directory contains the logic for generating LaTeX code.
*   **`tikzeng.py`:** The main engine. Defines functions like `to_Conv`, `to_Pool`, `to_head`, `to_end` that return LaTeX strings for specific network components.
*   **`blocks.py`:** Defines composite blocks (e.g., `block_2ConvPool`) that group multiple layers into reusable units.

### 2. LaTeX Styles (`layers/`)
Contains the underlying TikZ styles and definitions.
*   `Ball.sty`, `Box.sty`: Define the visual appearance of layers.
*   `init.tex`: Initial LaTeX setup imported by generated files.

### 3. Build Script (`tikzmake.sh`)
A shell script that automates the workflow:
1.  Runs the specified Python script to generate a `.tex` file.
2.  Compiles the `.tex` file using `pdflatex`.
3.  Opens the resulting PDF.

## Usage Guide

### Creating a New Diagram
1.  Create a new Python file (e.g., `my_arch.py`).
2.  Import the necessary modules:
    ```python
    import sys
    sys.path.append('../') # Ensure pycore is in path
    from pycore.tikzeng import *
    ```
3.  Define the architecture as a list of layer objects:
    ```python
    arch = [
        to_head('..'),
        to_cor(),
        to_begin(),
        to_Conv("conv1", 512, 64, offset="(0,0,0)", to="(0,0,0)", height=64, depth=64, width=2),
        # ... other layers ...
        to_end()
    ]
    ```
4.  Generate the file:
    ```python
    def main():
        namefile = str(sys.argv[0]).split('.')[0]
        to_generate(arch, namefile + '.tex')

    if __name__ == '__main__':
        main()
    ```

### Building
Run the helper script from the directory containing your python script (assuming `tikzmake.sh` is in the parent directory):
```bash
bash ../tikzmake.sh my_arch
```
*Note: Do not include the `.py` extension in the argument.*

## Development & Customization
*   **Adding Layers:** Modify `pycore/tikzeng.py` to add new Python functions that output corresponding TikZ code.
*   **Styling:** Edit files in `layers/` to change the visual look (colors, shapes) of the diagram components.
*   **Reusable Blocks:** Add new functions to `pycore/blocks.py` to create macros for common layer patterns.
