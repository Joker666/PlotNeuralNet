# Repository Guidelines

## Project Structure & Module Organization
- `pycore/`: Python helpers that emit TikZ/LaTeX (e.g., `tikzeng.py`, `blocks.py`).
- `layers/`: TikZ style definitions (`*.sty`, `init.tex`) used by generated diagrams.
- `pyexamples/`: Python example scripts (e.g., `test_simple.py`, `unet.py`).
- `examples/`: Prebuilt LaTeX examples and assets for common architectures.
- `tikzmake.sh`: Convenience script to run a Python example and build a PDF.

## Build, Test, and Development Commands
- `cd pyexamples && bash ../tikzmake.sh test_simple`: Runs `test_simple.py`, builds `test_simple.pdf`, and opens it.
- `python my_arch.py && pdflatex my_arch.tex`: Manual build flow if you prefer explicit steps.
- LaTeX dependencies: make sure a full TeX distribution is installed (see `README.md` for package lists).

## Coding Style & Naming Conventions
- Python uses 4-space indentation and snake_case functions (see `pycore/tikzeng.py`).
- Keep function signatures explicit and use simple string concatenation for TikZ blocks.
- LaTeX/TikZ styles live in `layers/`; keep style names consistent with existing `Box`, `RightBandedBox`, etc.

## Testing Guidelines
- No automated test suite is present.
- Validate changes by regenerating a PDF from a representative example in `pyexamples/` and visually inspecting the output.
- If you add a new layer or block, include a small example script demonstrating it.

## Commit & Pull Request Guidelines
- No strict commit convention is enforced; recent history uses short, imperative summaries.
- Include a brief PR description, and link related issues if applicable.
- For visual changes, attach a before/after PDF or screenshot (and note which example was used).

## Configuration Tips
- `tikzmake.sh` removes intermediate `.aux`, `.log`, and `.tex` files; keep any hand-written `.tex` files outside the working directory if you don’t want them deleted.
