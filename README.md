# WooWoo VSCode

This extension brings the **WooWoo Language Server** to VSCode. In addition to that, it provides basic client-side syntax highlighting.


![Find All References](images/find-all-references.png)

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
    - Install the WooWoo extension from the [VS Code Marketplace](https://marketplace.visualstudio.com/items?itemName=michal-janecek.woowoo-vscode) or [Open VSX](https://open-vsx.org/extension/michal-janecek/woowoo-vscode).

4. **Open Command Menu**:
    - Press `Ctrl + Shift + P` (Windows/Linux) or `Cmd + Shift + P` (Mac) and search for the `Python: Select Interpreter` command.

5. **Select Interpreter**:
    - Choose the Python interpreter where you installed `wuff` in step 2.
    - Alternatively, set the `woowoo-vscode.interpreter` setting to the path of that interpreter.

6. **Finalize Setup**:
    - Your setup is complete! If needed, specify the dialect you are using (refer to the _Dialect Configuration_ section for details).
    - If the language server isn't working, run the `WooWoo VSCode: Restart Server` command from the command menu.


### Dialect Configuration

Language support in WooWoo is highly dependent on the specific dialect used. To ensure the extension operates correctly, you must specify your dialect unless you're using the default `FIT-Math` dialect.

1. **Access Settings**: Open VSCode settings with `Ctrl + ,` (Windows/Linux) or `Cmd + ,` (Mac).
2. **Search for WooWoo**: Type `WooWoo` in the settings search bar.
3. **Set Dialect File Path**: Find the `WooWoo-vscode: Dialect_file_path` setting and input the absolute path to your `.yaml` dialect file.
4. **Done**: The language server restarts with the new dialect.

The dialect file path you set is passed to the language server when it starts.


## Language Server Features

Please visit [the official WooWoo Language Server repository](https://github.com/woowoo-dev/woowoo-language-server) to see the full list of features.


## Theme Choice and Semantic Highlighting

The choice of theme in VSCode plays a pivotal role in the semantic highlighting experience provided by the WooWoo LS. Some themes might use the same color for various token types, which could lead to suboptimal highlighting when working with WooWoo documents.


## Development

```bash
git clone --recurse-submodules https://github.com/woowoo-dev/vscode-woowoo-lsp.git
cd vscode-woowoo-lsp
python -m pip install nox
nox -s build_package   # bundles the Python libraries and builds woowoo-vscode.vsix
```

The language server is the `bundled/tool/woowoo_pygls` submodule
([woowoo-language-server](https://github.com/woowoo-dev/woowoo-language-server)).

To release, bump `version` in `package.json`, add a section to `CHANGELOG.md` and create a
GitHub release with the tag `vX.Y.Z`. The *Publish* workflow attaches the VSIX to the release
and, after an approval in the `marketplace` environment, publishes it to the VS Code
Marketplace and Open VSX.
