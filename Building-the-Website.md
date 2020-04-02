This documents the way the website is built and deployed with Netlify. 

_For how to deploy historical versions to GitHub pages visit https://github.com/vmware/clarity/wiki/Building-the-Website-with-GitHub-Pages._

# Previewing locally

The website is part of the project, inside of `src/website`. As part of your development, you can preview the website at any time by running the following and previewing it at http://localhost:4200. 

```bash
npm run website:start
```

This does only a local preview, which does not include prerendering the application for SEO and speed.

### Local prerendering

If you'd like to preview the website after it has been prerendered, you can do this by running the following command, which will run the build and start a local server at http://localhost:3000.

```bash
npm run website:prerender
npm run website:preview
```

Since this is quite slow, you typically want to do this only when necessary. Also, there is no way to watch for changes and rebuild, since it takes so long to prerender, so if you make changes you'll have to use `npm run website:prerender` command again to refresh the assets.

# Downloadable assets

Any large assets, such as icon zips and Sketch files are meant to be kept in the https://github.com/vmware/clarity-assets repository. The website links to these files directly to spare the complexity of hosting these files in our main repository project.

For images that we use in our documentation, those remain in the `clarity` repository under the `src/website/src/assets` directory.

# Adding a new release

To add a new release, you need to update a few files and create a release template.

* `src/website/src/releases/{MAJOR}/{VERSION}.html` - Add a new html file at this location with the release notes (usually easiest to copy an existing one and update it).
* `src/website/src/releases/release-list.json` - If this release is the new latest version, update the `current` property at the top with the new version number. Then add a new object to `all` in the same format with a date, sketch file version, and the commit ID of the release commit.
* `src/website/src/releases/release-template-stub.json` - Add a new line to this file with the version number and the file path to the HTML file.

# Versioning

## v3
To edit the v3 website or documentation use the [website](https://github.com/vmware/clarity/tree/master/src/website) folder on the master branch. Commits merged into the master branch will trigger an automatic deploy for Netlify.

## v2
To edit the v2 website or documentation use the [website](https://github.com/vmware/clarity/tree/master/src/website) folder on the v2 branch. Commits merged into the v2 branch will trigger an automatic deploy for Netlify.

## v1
To edit the v1 documentation use the [website](https://github.com/vmware/clarity/tree/v1/src/website) folder on the v1 branch. Commits merged into the v1 branch will trigger an automatic deploy for Netlify.

# Website scripts

In our package.json file, there are a set of scripts that are all prefixed with `website`. This is what each of them does.

* `website:compile` - This compiles the server and prerender scripts from TypeScript to JavaScript so we can run with with Node.
* `website:server` - This runs the server which has the web application embedded inside, allowing it to take requests and return a compiled route.
* `website:build` - This runs the website build process, which includes a prod build of the website, a production build of the server, and compiles the server and prerender scripts.
* `website:start` - This starts the local server for development, but also ensures you've built the news template first.
* `website:render` - This runs the prerender script that ultimately outputs the precompiled index.html files.
* `website:news` - This generates the news template files, which needs to be run whenever you change the releases information.
* `website:prerender` - This runs the news, build, and render steps to do a complete prerendering process.
* `website:preview` - This starts a local server for previewing the prerendered site.

# Deploying the Website

The website now runs on Netlify, so you'll need an account first, if you don't check with the Clarity team to get added (only for Clarity team maintainers).

Log into Netlify, and navigate to the Clarity project, then to the **Deploys** tab. There is a **Trigger deploy** button, which has two options **Deploy site** and **Clear cache and deploy site**. Usually the **Deploy site** is sufficient, but if there are build errors you can use the cache clear option as well. 

Once you run a deploy it will run and be immediately available upon completion.

We do not have automatic deploys turned on, so please do not turn it on at this time.