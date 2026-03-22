# subnets
Visual subnet calculator as seen at http://www.davidc.net/sites/default/subnets/subnets.html

## GitHub Pages

This site is hosted as a static site via GitHub Pages. To enable it, go to your repository **Settings → Pages**, set the source to the `main` branch and `/ (root)` folder, then save.

## Run with docker

```
cd <project folder>
docker build . -t subnets
docker run -d -p 5001:80 --name subnets subnets
```
