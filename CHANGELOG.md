# Change Log

All notable changes to the WooWoo VS Code extension are documented here.

## [1.4.0] - 2026-11-01

### Added

- Bibliography support (language server 1.3.0, needs `wuff` 1.4.0). If the project's
  `Woofile` names a BibTeX file (`builder.bibtex`), `.cite:` suggests its keys with the
  authors, year and title, Ctrl+click on a key opens the entry in the `.bib` file, hover
  shows the entry, and an unknown key gets a warning.
- Completion inside a reference that is already partly typed (Ctrl+Space on
  `.reference:sec-`), and find references and rename from any reference, not only from
  the label.
- With a `wuff` older than 1.4.0 the extension shows *wuff X is too old … Run:
  pip install -U wuff* instead of failing.

### Changed

- `.eqref:` and the `#` shorthand also offer and open the labels of `align` and `gather`.

### Fixed

- Completion after Czech (non-ASCII) text on the same line, and go to definition that
  pointed a character or two next to the label.
- Files with capital letters in their name (`chap-09-OLS.woo`) on macOS and Windows: the
  server kept a second, outdated copy of such a file, which could show up in find
  references, rename and `.include` completion.
- Ctrl+click on an `.include` of a file that does not exist no longer shows
  *Error in server*.

## [1.3.1] - 2026-11-01

### Fixed

- The language server no longer crashes on start with Python 3.15. The bundled
  `typing-extensions` 4.9.0 uses `typing.no_type_check_decorator`, which Python 3.15
  removed; the extension now bundles `typing-extensions` 4.16.0 and `exceptiongroup` 1.3.1.
- Changing the `woowoo-vscode.dialect_file_path` setting restarts the language server, so
  the new dialect applies without restarting VS Code.
- README: the screenshot points to this repository, and the setup steps link the
  Marketplace and Open VSX pages and mention the `woowoo-vscode.interpreter` setting.

### Removed

- The Python tests and the `test` npm script inherited from Microsoft's extension template.
  They tested a sample Python linter, not this extension.

## [1.3.0] - 2026-10-31

### Added

- Syntax highlighting for the body of the `equation`, `align` and `gather` outer
  environments, using the same scope as inline math (`constant.numeric`). Standalone
  formulas used to be highlighted as ordinary text. Meta blocks attached to these
  environments — below the header and below a block — keep their normal highlighting.
- LaTeX-level highlighting inside math, i.e. inside `$…$` and inside the bodies of
  `equation`, `align` and `gather`: commands such as `\frac` or `\sin` (`support.function`),
  `\begin`/`\end` (`keyword.control`) with the environment name (`entity.name.type`),
  `^`, `_`, `=`, `<>`, `+ - * / & |` and `\\` (`keyword.operator`), the argument of
  `\text{…}` (`string`) and an indented `%` comment (`comment.line`). Braces keep the
  surrounding colour.
- Indented blocks (anonymous formulas in the FIT math dialect) get the same LaTeX
  highlighting as inline math, at document level and inside wobject bodies such as
  `.Definition:` or inside `.itemize:`/`.item:` lists. They have no header line and TextMate
  cannot tell such a block from a prose line of the enclosing environment, so wuff reports
  them as semantic tokens instead, mirroring the `#latex` rules with standard token types
  (`number` for plain math, `function` for commands, `operator`, `string` for the argument of
  `\text{…}`, `type` for the environment name, `comment` for `%`). `semanticTokenScopes`
  maps those types to the scopes the grammar uses inside `$…$`, so both render with the same
  colours and no per-token-type configuration is needed. The only difference is `\begin`/`\end`,
  which use the command scope (`support.function`) instead of `keyword.control`, because the
  `keyword` type is already used for `.include` lines. Requires `wuff` 1.3.0 or newer and
  language server v1.2.0, whose FIT-Math dialect marks `equation`/`align`/`gather` with
  `math: true`.
- Richer hover hints, delivered by the updated language server: the hint is Markdown and
  lists the meta-block fields of the hovered part, wobject or environment with a short help
  text for the non-obvious ones, and tells you when the fragile form (`!tikz:`) is needed.
  Requires `wuff` 1.3.0 or newer and language server v1.2.0.

### Changed

- The extension requires Python 3.10 or newer, matching `wuff` 1.3.0, which dropped 3.8 and
  3.9 as end of life. `checkVersion` rejects such interpreters instead of letting the server
  fail on `import wuff`, the missing-interpreter message and the README say 3.10, and
  `runtime.txt` names `python-3.10.22`.
- Development dependencies are refreshed within their declared ranges (TypeScript 5.9.3,
  webpack 5.112.2, ESLint 8.57.1) and `@vscode/vsce` is 4.0.0; packaging the extension now
  needs Node 22 or newer. The extension itself is unaffected: `npm audit --omit=dev`
  reports no vulnerabilities. The two advisories that remain concern `@azure/msal-node`,
  which vsce pulls in for publishing credentials, and cannot be fixed until
  `@azure/identity` moves to `@azure/msal-node` 7.
