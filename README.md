# tln-vscode

[Visual Studio Code](https://code.visualstudio.com/) extension for the
[Tln](https://github.com/opentalon/tln-language) expert-system rule
language.

Provides:

- **Syntax highlighting** for every block type, clause, ML primitive,
  template interpolation, and reserved keyword in the Tln grammar.
- **File-type detection** for `*.tln` and `*.tln.test`.
- **Editor configuration** — `//` toggle-comment, brace auto-close +
  auto-indent, folding markers on top-level blocks.

## Install

### Locally (from this repo)

Clone and drop into your VS Code extensions directory:

```bash
git clone https://github.com/opentalon/tln-vscode \
  ~/.vscode/extensions/opentalon.tln-vscode-0.1.0
```

Reload VS Code (`Developer: Reload Window` from the command palette).
Any `.tln` or `.tln.test` file now highlights.

### From the Marketplace

```bash
code --install-extension opentalon.tln-vscode
```

Once published — see [tracking issue](https://github.com/opentalon/tln-language/issues/18).

## Verify

Open any Tln file:

```bash
code examples/insurance_claims.tln
```

You should see:

- `rule`, `detect`, `recommend` block headers coloured as keywords.
- String literals coloured, with `{item.name}` placeholders picking up
  a distinct interpolation highlight.
- `//` and `/* */` comments dimmed.
- Press `Cmd+/` (`Ctrl+/`) inside a block — toggles `//` comments.
- Type `{` — auto-closes; the next line auto-indents two spaces.

Status bar (bottom right) should read **Tln**. Run
**Change Language Mode** from the command palette to confirm.

## Layout

```
tln-vscode/
├── package.json                       # extension manifest
├── language-configuration.json        # brackets, comments, indent rules
├── syntaxes/
│   └── tln.tmLanguage.json          # TextMate grammar
├── README.md
└── LICENSE
```

## Staying in sync with the language

The keyword list mirrors
[`internal/lexer/lexer.go`](https://github.com/opentalon/tln-language/blob/master/internal/lexer/lexer.go)
in the language repo. When upstream adds a new keyword, mirror it into
the relevant pattern in `syntaxes/tln.tmLanguage.json` here — one
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

- [opentalon/tln-vim](https://github.com/opentalon/tln-vim) — sister plugin for Vim / Neovim.
- [opentalon/tln-language](https://github.com/opentalon/tln-language) — the language itself, compiler, runtime.

## License

Apache 2.0 — matches [tln-language](https://github.com/opentalon/tln-language).
