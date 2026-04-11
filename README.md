# sose26-real-world-problems-ai

## Build the Jupyter Book (MyST)

From the repository root, with the project virtual environment activated:

```bash
jupyter-book build --site --html --execute
```

Do **not** run `jupyter-book build .` — the `.` is treated as a file to export, which triggers `EISDIR` (reading a directory as a file).

- **`--site`** — build the book navigation and pages from `myst.yml`
- **`--html`** — emit static HTML (default output under `_build`)
- **`--execute`** — run notebooks during the build (optional; omit for faster builds)

Live preview while editing:

```bash
jupyter-book start
```