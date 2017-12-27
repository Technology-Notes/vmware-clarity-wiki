This documents the way the website is built and deployed with GitHub Pages.

# Suggested directory structure

```
/website - checkout `website-ssr` (or `new-website` after merged)
/gh-pages - checkout `gh-pages`
/v0.10-website - checkout `v0.10-website`
```

# To build v0.10

The v0.10 website is now _only_ the content of the documentation. This is required to get the routing working correctly. This means there are a few changes to this website that diverge from the main website, so take note.

```
cd ./v0.10-website
npm run build:deploy
```

This will generate the assets and place them inside of the `/gh-pages/documentation/v0.10`.

To test locally, use the following.

```
npm start # This is for local dev like normal

npm run build:static # This prerenders but doesn't drop into `gh-pages` directory
npm run serve:static # This serves the static assets
```

# To build v0.11

This is the normal website, but it has been changed to host the documentation assets at the file paths of the current version. Other versions are placed alongside it.

```
cd ./website
npm run build:deploy
```

This will generate the assets and place them inside of the `/gh-pages`.

To test locally, use the following.

```
npm start # This is for local dev like normal

npm run build:static # This prerenders but doesn't drop into `gh-pages` directory
npm run serve:static # This serves the static assets
```

# To test `gh-pages`

Just run a static server from the gh-pages directory like so.

```
cd ./gh-pages
python -m SimpleHTTPServer
```
