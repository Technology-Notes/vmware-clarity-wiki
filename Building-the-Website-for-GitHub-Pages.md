> # THIS IS ONLY FOR HISTORICAL PAGES DEPLOYED ON GITHUB PAGES. FOR CURRENT WEBSITE BUILD DETAILS, VISIT https://github.com/vmware/clarity/wiki/Building-the-Website.

***


This documents the way the website is built and deployed with GitHub Pages. Our website is now versioned, and the different versions of the website are kept together in the `website` branch.

Inside of this branch there are two basic directories

`latest` - This contains the latest version of the website, including the home, community, news pages.
`v0.10` - This contains the version for v0.10 documentation. (Other folders may exist for other versions as well)

# Setup local environment

To properly build and run the site, you'll start by cloning the repo and checking out the website branch. Then you'll need to setup each of the versions that you plan to preview and build. The script below could be used in a *nix environment. Open the terminal, navigate to this new directory and run the following.

```
git clone -b website https://github.com/vmware/clarity.git website
cd website
npm install
cd latest
npm install
cd ../v0.10
npm install
```

Each directory is essentially its own version of the website so each has its own node modules. If new versions are added, you'll need to run `npm install` inside of that directory as well.

This gets the necessary assets ready for building, previewing, and deploying the website.

# Local preview of final build

If you have the folder structure as outlined above, then you can easily build and preview the website locally. To do this you must start by building the static files for each version. The `npm run deploy` command is used inside of each version directory to build the assets and drops them inside of the `./clarity` directory (which is ignored by git).

```
cd ./latest
npm run deploy
cd ../v0.10
npm run deploy
```

Once this is done, you can run `npm start` from the parent directory (where the package.json file and the directories live) and it will start a local server. You have to go to `http://localhost:8080/clarity` to see the website locally (because on GitHub it is hosted at the path /clarity, this emulates that correctly locally).

Every time you make file changes you have to run the `npm run deploy` command from the directory you made changes, which can be slow. It is recommended to use dev mode (described below) when trying to make larger changes and only preview the static assets after you're more confident it is close to ready.

# Local dev development

You can preview the website locally by going to the directory with the latest website directory and running the following. 

```
cd ./latest
npm start
```

Then view `http://localhost:4200` to see the website in dev mode.

> Note, the version switcher does not currently work in dev mode.

# Adding new versions to website

* Copy the current `latest` directory to a new directory with the version name like `v1.0`.
* Update the `src/environments/environment.prod.ts` file with the correct `version` property.
* Copy the `v0.10/prerender.ts` script over the `newVersion/prerender.ts` script.
* Remove anything from the `news`, `community`, `releases`, `home`, `icons` directories. See `v0.10` for what was kept.
* Update the new version Angular routes so the documentation is now the root of the URL routing. See `v0.10` for how it was updated.