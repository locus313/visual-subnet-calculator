# Visual Subnet Calculator

A self-contained, single-page IPv4 subnet calculator. Enter a network address and prefix length, then interactively divide and join subnets to plan your address space. The current state is encoded in the URL so results can be bookmarked and shared.

Originally based on the calculator at http://www.davidc.net/sites/default/subnets/subnets.html

## Features

- Visual, tree-based subnet division and joining
- Displays subnet address, range, useable range, and host count per row
- Toggle individual columns on/off
- Shareable/bookmarkable URLs — full calculator state is encoded in the query string
- No build step, no dependencies — plain HTML and JavaScript

## Usage

Open `subnets.html` directly in a browser, or serve it from any static web host.

1. Enter a network address (e.g. `10.0.0.0`) and prefix length (e.g. `8`).
2. Click **Update** to load the base network.
3. Use the **Divide** button on any row to split a subnet into two equal halves.
4. Use the **Join** button to merge previously divided subnets back together.
5. Copy the URL to bookmark or share your current layout.

## GitHub Pages

This site is deployed automatically via GitHub Actions to the `gh-pages` branch on every push to `master`. To activate hosting, go to your repository **Settings → Pages**, set the source to the `gh-pages` branch and `/ (root)` folder, then save.

## File layout

| Path | Purpose |
|------|---------|
| `subnets.html` | Main calculator — all logic and UI inline |
| `index.html` | Entry point |
| `img/*.gif` | Pre-rendered subnet mask images (`0.gif` – `32.gif`) |
| `.github/workflows/deploy.yml` | GitHub Actions → GitHub Pages deployment |

## License

See [LICENSE.md](LICENSE.md).
