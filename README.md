# talon-vscode

[Visual Studio Code](https://code.visualstudio.com/) extension for the
[Talon](https://github.com/opentalon/talon-language) expert-system rule
language.

Provides:

- **Syntax highlighting** for every block type, clause, ML primitive,
  template interpolation, and reserved keyword in the Talon grammar.
- **File-type detection** for `*.talon` and `*.talon.test`.
- **Editor configuration** — `//` toggle-comment, brace auto-close +
  auto-indent, folding markers on top-level blocks.

## Install

### Locally (from this repo)

Clone and drop into your VS Code extensions directory:

```bash
git clone https://github.com/opentalon/talon-vscode \
  ~/.vscode/extensions/opentalon.talon-vscode-0.1.0
```

Reload VS Code (`Developer: Reload Window` from the command palette).
Any `.talon` or `.talon.test` file now highlights.

### From the Marketplace

```bash
code --install-extension opentalon.talon-vscode
```

Once published — see [tracking issue](https://github.com/opentalon/talon-language/issues/18).

## Verify

Open any Talon file:

```bash
code examples/insurance_claims.talon
```

You should see:

- `rule`, `detect`, `recommend` block headers coloured as keywords.
- String literals coloured, with `{item.name}` placeholders picking up
  a distinct interpolation highlight.
- `//` and `/* */` comments dimmed.
- Press `Cmd+/` (`Ctrl+/`) inside a block — toggles `//` comments.
- Type `{` — auto-closes; the next line auto-indents two spaces.

Status bar (bottom right) should read **Talon**. Run
**Change Language Mode** from the command palette to confirm.

## Layout

```
talon-vscode/
├── package.json                       # extension manifest
├── language-configuration.json        # brackets, comments, indent rules
├── syntaxes/
│   └── talon.tmLanguage.json          # TextMate grammar
├── README.md
└── LICENSE
```

## Staying in sync with the language

The keyword list mirrors
[`internal/lexer/lexer.go`](https://github.com/opentalon/talon-language/blob/master/internal/lexer/lexer.go)
in the language repo. When upstream adds a new keyword, mirror it into
the relevant pattern in `syntaxes/talon.tmLanguage.json` here — one
line in the matching category's regex alternation.

A future iteration may generate the grammar JSON directly from
`lexer.go` to avoid drift. Until then, the manual mirror is small and
infrequent — roughly one diff per merged language-feature PR.

## Publishing to the Marketplace (maintainer notes)

```bash
npm install -g @vscode/vsce
vsce package
vsce publish
```

Requires a [Microsoft publisher account](https://marketplace.visualstudio.com/manage)
under the `opentalon` publisher ID.

## Related

- [opentalon/talon-vim](https://github.com/opentalon/talon-vim) — sister plugin for Vim / Neovim.
- [opentalon/talon-language](https://github.com/opentalon/talon-language) — the language itself, compiler, runtime.

## License

Apache 2.0 — matches [talon-language](https://github.com/opentalon/talon-language).
