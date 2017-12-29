# Clarity v0.11.0 Breaking Changes
Clarity has changed to scoped packages starting at v0.11.0. There were several reasons for changing to scoped packages them largest and most important being to remove the word `clarity` from file-paths and filenames so that Clarity would not get blocked by Easylist (commonly used in ad blockers). 

This  means that there are changes needed for an application that consumes Clarity. Here, we will use a typical Angular Cli application to describe the changes needed to upgrade to Clarity v0.11.0. We will assume that the application is set up similar to the [clarity-seed](https://github.com/vmware/clarity-seed) application. 

## (Re) Installing Clarity
Clarity packages (angular, icons and ui) are now published under the `@clr` scope. This means you will need to uninstall the old clarity packages with npm and re-install clarity@0.11.0 from `@clr`.

**Using `npm` on your command line uninstall the old clarity sources:**

```
$ npm uninstall clarity-angular clarity-icons clarity-ui --save-dev
```

**Using `npm` on your command line install the Clarity scoped packages.** 

```
$ npm install @clr/angular @clr/icons @clr/ui --save-dev
```

This will do two things.

1. It will remove the old clarity sources from your `node_modules`
2. It will update your packages.json devDependencies

## Modify `.angular-cli.json`
ClarityIcons (css & js) and ClarityUI (css) files are bundled into an angular-cli application with the .angular-cli.json configuration file. 

**Typical v0.10.X `angular-cli.json` configuration**

```
...
"styles": [
        "../node_modules/clarity-icons/clarity-icons.min.css",
        "../node_modules/clarity-ui/clarity-ui.min.css",
        ...
      ],
      "scripts": [
        ...
        "../node_modules/clarity-icons/clarity-icons.min.js"
      ],
  ...
```

**Updated v0.11.0 `.angular-cli.json` configuration**

```
...
"styles": [
                "../node_modules/@clr/icons/clr-icons.min.css",
                "../node_modules/@clr/ui/clr-ui.min.css",
                "styles.css"
            ],
            "scripts": [
                ...
                "../node_modules/@clr/icons/clr-icons.min.js",
                ...
            ],
...
```

**NOTE: Both the filepath and the source filename have changed**

## Update Clarity Imports
Clarity is now following the [Angular Package Format](https://docs.google.com/document/d/1CZC2rcpxffTDfRDs6p1cfbmKNLA6x5O-NtkJglDaBVs/preview) in order to support consumption in a variety of ways that use common build and bundling tools in use today.

This means Clarity applications upgrading to v0.11.0 will need to update the [non-relative](https://www.typescriptlang.org/docs/handbook/module-resolution.html) module paths in their application sources. 

**Clarity v0.10.0 import statement**

```
import { thing } from "clarity-angular";
```

**Clarity v0.11.0 import statement**

```
import { thing } from "@clr/angular";
```

# v0.11 Deprecations

All object names now conform to our naming conventions. We've deprecated the existing names so you can upgrade without issue, but you will need to modify references to Clarity components and services.

The changes are simple and only names, but will help avoid naming collisions with other projects by using proper prefix `Clr` on anything we export. Here are some examples.

```
Wizard -> ClrWizard
Button -> ClrButton
State -> ClrDatagridStateInterface
SortOrder -> ClrDatagridSortOrder
```

## Thats All
Once the **.angular-cli.json** and **import** statements are updated for your application it should build and run just as it did before. If you have questions or issues for upgrading upir application then please reach out on StackOverflow with the tag **[vmware-clarity](https://stackoverflow.com/questions/tagged/vmware-clarity)** or on twitter **[@vmweareclarity](https://twitter.com/vmwareclarity)**. 