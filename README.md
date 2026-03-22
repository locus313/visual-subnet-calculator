# subnets
Visual subnet calculator as seen at http://www.davidc.net/sites/default/subnets/subnets.html

## GitHub Pages

This site is deployed automatically via GitHub Actions to the `gh-pages` branch on every push to `master`. To activate hosting, go to your repository **Settings → Pages**, set the source to the `gh-pages` branch and `/ (root)` folder, then save.

## Run with docker

```
cd <project folder>
docker build . -t subnets
docker run -d -p 5001:80 --name subnets subnets
```
