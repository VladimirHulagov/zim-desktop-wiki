# Agents Guide — zim-desktop-wiki

## Repository layout

- **Upstream**: `https://github.com/zim-desktop-wiki/zim-desktop-wiki.git` (remote `original`)
- **Fork**: `git@github.com:VladimirHulagov/zim-desktop-wiki.git` (remote `origin`)
- Main working branch: `develop`

## Code style (CRITICAL)

The project uses its own style defined in `.editorconfig`. **Never reformat existing code.**

- **Indentation**: **tabs**, not spaces (tab size = 4 spaces equivalent)
- **String quotes**: single quotes (`'...'`) preferred; double quotes only for strings containing single quotes or SQL
- **Docstrings**: triple single quotes (`'''...'''`), not triple double quotes
- **Line continuations**: backslash (`\`) style, not parenthesized multi-line imports
- **Trailing commas**: generally not used in upstream code
- **Comments**: `# comment` with one space after `#`; inline comments aligned with two spaces before `#`

Do **not** run autoformatters (black, autopep8, yapf, etc.) on this codebase — it will cause merge conflicts with upstream on every pull.

## Tests

Tests live in `tests/` and use `unittest` style (classes inheriting from `TestCase`).

Run a specific test file:
```
python3 -m pytest tests/indexviews.py
```

Run all tests:
```
python3 -m pytest tests/
```

## Key modules

- `zim/notebook/index/pages.py` — page index DB layer (`PagesIndexer`, `PagesView`, `PagesTreeModelMixin`)
- `zim/plugins/pageindex/__init__.py` — page index UI plugin (GTK TreeView)
- `zim/plugins/versioncontrol/` — version control plugin (git backend in `git.py`)
- `zim/plugins/journal.py` — journal/calendar plugin
- `zim/search.py` — search engine
- `zim/notebook/notebook.py` — core notebook logic

## GTK / UI notes

- Uses GTK 3 via `gi.repository` (GObject introspection)
- Custom `GenericTreeModel` for tree views — manages its own memory (no leak-references)
- Signals follow GObject convention: `'signal-name'` with dashes

## Merge workflow

When merging from upstream (`original`), expect no formatting changes in our commits.
Keep all local modifications in the upstream code style (tabs, single quotes, etc.).
