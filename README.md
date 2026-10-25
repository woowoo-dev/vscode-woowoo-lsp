# WooWoo VSCode

This extension brings the **WooWoo Language Server** to VSCode. In addition to that, it provides basic client-side syntax highlighting.


![alt text](https://raw.githubusercontent.com/Magmi183/vscode-woowoo-lsp/main/images/find-all-references.png)

## Prerequisites

- Python 3.10 or higher


## Installation Guide

Please follow these steps to set up the extension:

1. **Check System Compatibility**: 
    - The extension is compatible with most systems running Python 3.10 or higher.
    - On non-standard systems, a C++ compiler is required to compile the `wuff` package.

2. **Install `wuff`**:
    - Install the `wuff` package into the Python interpreter that the extension will use to launch the language server. This could be a Python virtual environment, the system-wide Python installation, or any other Python interpreter on your system.
    - Use `pip install wuff` to install. `wuff` is a set of analyzer tools for WooWoo projects, developed in C++ for efficiency.
    - The package is available on [PyPI](https://pypi.org/project/wuff/#files).

3. **Install Extension**:
    - Install the WooWoo extension from the VSCode Marketplace.

4. **Open Command Menu**:
    - Press `Ctrl + Shift + P` (Windows/Linux) or `Cmd + Shift + P` (Mac) and search for the `Python: Select Interpreter` command.

5. **Select Interpreter**:
    - Choose the Python interpreter where you installed `wuff` in step 2.

6. **Finalize Setup**:
    - Your setup is complete! If needed, specify the dialect you are using (refer to the _Dialect Configuration_ section for details).
    - If the language server isn't working, run the `WooWoo VSCode: Restart Server` command from the command menu.


### Dialect Configuration

Language support in WooWoo is highly dependent on the specific dialect used. To ensure the extension operates correctly, you must specify your dialect unless you're using the default `FIT-Math` dialect.

1. **Access Settings**: Open VSCode settings with `Ctrl + ,` (Windows/Linux) or `Cmd + ,` (Mac).
2. **Search for WooWoo**: Type `WooWoo` in the settings search bar.
3. **Set Dialect File Path**: Find the `WooWoo-vscode: Dialect_file_path` setting and input the absolute path to your `.yaml` dialect file.
4. **Restart VSCode**: To apply the changes, restart VSCode.

The dialect file path you set is passed to the language server by the VSCode language server client upon startup.


## Language Server Features

Please visit [the official WooWoo Language Server repository](https://gitlab.fit.cvut.cz/woowoo/lsp/woowoo-language-server) to see the full list of features.


## Theme Choice and Semantic Highlighting

The choice of theme in VSCode plays a pivotal role in the semantic highlighting experience provided by the WooWoo LS. Some themes might use the same color for various token types, which could lead to suboptimal highlighting when working with WooWoo documents.

