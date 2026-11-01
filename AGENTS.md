# AGENTS.md

The WooWoo extension for VS Code: a TypeScript language client, a TextMate grammar and the
[WooWoo Language Server](https://github.com/woowoo-dev/woowoo-language-server), which is the
git submodule `bundled/tool/woowoo_pygls`. The server's Python dependencies (pygls and co.) are
bundled in `bundled/libs`; [wuff](https://github.com/woowoo-dev/wuff), the C++ analysis engine,
is not bundled: users `pip install wuff` into the interpreter the extension uses.

## Build and test

```bash
git submodule update --init
python -m pip install nox
nox -s build_package   # bundles requirements.txt into bundled/libs, npm ci, builds woowoo-vscode.vsix
npm run lint
```

The *CI* workflow runs on every PR: lint, VSIX build (downloadable as the `vsix` artifact) and
the language server smoke test against the bundled server on Python 3.10 to 3.15.

## Layout

- `src/`: the language client; `src/extension.ts` starts it, `src/common/settings.ts` reads
  the `woowoo-vscode.*` settings.
- `syntaxes/`: the TextMate grammar (client-side highlighting); `package.json` maps the
  server's semantic token types to TextMate scopes (`semanticTokenScopes`).
- `bundled/tool/lsp_server.py`: puts `bundled/libs` and the submodule on `sys.path` and starts
  the server.
- `requirements.in` → `requirements.txt` (pip-compile with hashes) → `bundled/libs`.

## Rules

- Server changes belong in the woowoo-language-server repository. Here, move the submodule to
  the new commit or tag.
- `pygls` stays at 1.3.0 (pinned in `requirements.in`, matching the language server's
  `requirements.txt`). pygls 2 needs a port of the server.
- Update `requirements.txt` with pip-compile on Python 3.10 (see `requirements.in`), never by
  hand.
- Record user-visible changes in `CHANGELOG.md`.
- Do not create releases or tags. A release is published from a GitHub release by the
  *Publish* workflow after a maintainer's approval (see README, *Development*).
