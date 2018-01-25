This documents the way the website is built and deployed with GitHub Pages. Our website is now versioned, and the different versions of the website are kept in separate branches.

`new-website` - This contains the latest version of the website, including the home, community, news pages.
`v0.10-website` - This contains the version for v0.10 documentation.

If you only plan to make changes in the latest version, you don't need to worry about the other versions when you work with the website. However, if you plan to make changes to an older version, you will need to have the latest version as well to be able to build and preview it correctly.

# Setup local environment

To properly build and run the site, you'll need to setup a new directory. The script below could be used in a *nix environment. Open the terminal, navigate to this new directory and run the following.

```
git clone -b gh-pages https://github.com/vmware/clarity.git clarity
git clone -b new-website https://github.com/vmware/clarity.git latest
git clone -b v0.10-website https://github.com/vmware/clarity.git v0.10
cd latest && npm i && npm run generate-release-notes && npm run build
cd ../v0.10 && npm i
cd ../
cat <<EOT>> package.json
{
  "name": "clarity",
  "version": "0.0.0",
  "scripts": {
    "start": "http-server ."
  },
  "private": true,
  "devDependencies": {
    "http-server": "latest"
  }
}
EOT
npm i
```

The result should be like the following:

```
/clarity - copy of the `gh-pages` branch
/latest - checkout `new-website`
/node_modules - node modules
/v0.10 - checkout `v0.10-website`, which is only necessary if you are going to update old versions of the docs
/package.json - file that contains basic npm scripts to run a local server
```

This gets the necessary assets ready for building, previewing, and deploying the website.

# Local preview of final build

If you have the folder structure as outlined above, then you can easily build and preview the website locally. To do this you must start by building the static files for each version. The `npm run deploy` command is used inside of each version directory to build the assets and drops them inside of the `./clarity` directory.

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

# Local prerendering development

You can also preview the local prerendering mode, which is similar to the dev mode except that it builds the static assets and serves them instead. You usually don't need to use this, but it is available.

```
cd ./v0.10-website        # navigate to the version directory
npm run build:static      # run the build command that generates the static assets
npm run serve:static      # run the serve command to view the static assets locally
```

You can also run the `serve:static` command in one terminal and then run the `build:static` in another terminal to refresh the static assets as you make changes. There is no watch mode however.
