_disclaimer: this guide was created under the context of me trying to get Croissant working on my Windows machine. It's in no mean meant to be comprehensive and will likely receive limited updates._

# Croissant WSL Guide

This guide will help you set up [Croissant](https://github.com/mlcommons/croissant) on Windows using WSL.

## Why WSL?

Because as much as I tried to get Croissant working natively on Windows with miniconda, I just couldn't. WSL is a great way to run Linux applications on Windows without the overhead of a full VM.

If anyone knows how to get Croissant working natively on Windows, please let me know!

## Prerequisites

1. **Windows Subsystem for Linux (WSL)**: Make sure you have WSL installed. You can follow the official [Microsoft guide](https://docs.microsoft.com/en-us/windows/wsl/install) to set it up. For the record, I'm using Ubuntu 22.04.2.

2. **Python**: Make sure you have Python installed in your WSL environment. From [the Croissant repo](https://github.com/mlcommons/croissant), it seems that anything >=3.10 should work. I'm using Python 3.10.12.

3. **pip**: Ensure you have pip installed to manage Python packages. You can install it using:

   ```bash
   sudo apt update
   sudo apt install python3-pip
   ```

## Steps

1. From PowerShell, install WSL and set up your preferred Linux distribution (e.g., Ubuntu):

   ```powershell
   wsl --install
   ```

2. Open your WSL through PowerShell or the Start Menu. If going through PowerShell, you can do:

   ```powershell
   wsl
   ```

3. Just check that Python and pip is installed and is the right version:

   ```bash
   python3 --version
   pip3 --version
   ```

4. Create a virtual environment. Of course, any name works, but I'll use `croissant-env` here:

   ```bash
   python3 -m venv croissant-env
   source croissant-env/bin/activate
   ```

5. You'll first need to manually install `GitPython` and `mlcroissant[parquet]`. This one comes from [the Hugging Face instructions](https://huggingface.co/docs/dataset-viewer/mlcroissant):

   ```bash
   pip install GitPython mlcroissant[parquet]
   ```

6. On [the Croissant repo](https://github.com/mlcommons/croissant), you'll find the following code snippet:

   ```python
   import mlcroissant as mlc
   ds = mlc.Dataset("https://raw.githubusercontent.com/mlcommons/croissant/main/datasets/1.0/gpt-3/metadata.json")
   metadata = ds.metadata.to_json()
   print(f"{metadata['name']}: {metadata['description']}")
   for x in ds.records(record_set="default"):
       print(x)
   ```

   Run that. It should work.

7. (optional) On the Croissant repo you'll also find an [introduction.ipynb](https://github.com/mlcommons/croissant/blob/main/python/mlcroissant/recipes/introduction.ipynb), which is a bit more comprehensive. You can run it using Jupyter Notebook or Jupyter Lab. To install Jupyter, run:

   ```bash
   pip install jupyterlab
   jupyter lab
   ```
