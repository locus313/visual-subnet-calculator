# Copilot Instructions — Visual Subnet Calculator

## Project overview

A self-contained, single-page IPv4 subnet calculator built with plain HTML and vanilla JavaScript. No build tools, no package manager, no external dependencies.

Live site: deployed via GitHub Actions to GitHub Pages on every push to `master`.

## File layout

| Path | Purpose |
|------|---------|
| `subnets.html` | Main calculator — all logic and UI inline |
| `index.html` | Entry point (mirrors or redirects to subnets.html) |
| `img/*.gif` | Pre-rendered mask images (named `0.gif` … `32.gif`) |
| `.github/workflows/deploy.yml` | GitHub Actions → gh-pages deployment |

## Architecture

All JavaScript lives **inline** inside the HTML files — there are no separate `.js` files. Keep it that way unless explicitly asked to extract scripts.

### Subnet tree data structure

Subnets are stored as a recursive 3-element array:

```
node = [depthOfChildren, numVisibleChildren, childrenArrayOrNull]
```

- Leaf node: `[0, 0, null]`
- Divided node: `[depth, count, [leftChild, rightChild]]`

Key functions in `subnets.html`:

| Function | Role |
|----------|------|
| `divide(node)` | Splits a subnet into two halves |
| `join(node)` | Merges two halves back |
| `recreateTables()` | Full DOM re-render from root |
| `createRow(...)` | Recursive row builder |
| `nodeToString` / `binToAscii` / `asciiToBin` | URL state serialisation |
| `inet_aton` / `inet_ntoa` | IP ↔ integer conversion |
| `network_address`, `subnet_addresses` | Bitwise subnet math |

### URL-based state

Calculator state (network, mask, division tree) is encoded in the query string so results can be bookmarked:

```
subnets.html?network=10.0.0.0&mask=8&division=<encoded>
```

## Design / Styling

Both HTML files share an identical inline `<style>` block with a dark theme built on CSS custom properties:

| Variable | Purpose |
|----------|---------|
| `--bg` | Page background (`#0f172a`) |
| `--surface` / `--surface2` | Card and header backgrounds |
| `--border` | Border colour |
| `--accent` | Sky-blue highlight (`#38bdf8`) used for links, focus rings, buttons |
| `--text` / `--text-muted` | Primary and secondary text |
| `--join-bg` / `--join-hover` | Join-column cell backgrounds |

Key layout / component classes:

| Class | Purpose |
|-------|---------|
| `.site-header` | Top bar with title and GitHub link |
| `.control-panel` | Rounded card containing the form |
| `.input-row` | Flexbox row for network inputs and buttons |
| `.toggle-chip` | Pill-shaped column-visibility checkbox |
| `.table-wrapper` | Rounded, scrollable container for the subnet table |
| `.btn-primary` / `.btn-secondary` | Styled form buttons |
| `.maskSpan` / `.maskSpanJoinable` | Join-column cells; GIF images inside are inverted via `filter: invert(1) opacity(0.85)` so they read on the dark background |

When editing or adding styles, use the existing CSS variables rather than hard-coded colours. Keep all styles inline — no external stylesheet.

## Conventions

- **No build step** — edits to HTML/JS are immediately reflected in a browser.
- **No linter or formatter** is configured; match the surrounding style (2-space indent, `var` declarations, legacy `function` style).
- **GIF images are pre-generated** — do not expect to create new ones at runtime. Adding support for masks outside 0–32 would require new images.
- `visibleColumns` object in both HTML files controls which table columns are shown; toggling columns should update that object and call `recreateTables()`.
- **Keep both files in sync** — `subnets.html` and `index.html` are near-identical; changes to one (styles, markup, JS) should be mirrored in the other.

## Deployment

Push to `master` → GitHub Actions runs `.github/workflows/deploy.yml` → published to `gh-pages` branch → served by GitHub Pages.

No manual deploy step is needed. To test locally, open the HTML file directly in a browser.
