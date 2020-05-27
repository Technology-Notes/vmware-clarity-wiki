This page describes the steps to follow when releasing a new version of Clarity. The basic flow is to organize the tickets in GitHub, test the build, add release information, and publish.

# GitHub Organization

### Milestones

1. Create a new milestone for the next expected version (usually next patch, can always be edited).
2. Look at the milestone for the version you are releasing.
    * Compare the commits in master to find any PRs that might be missing and link them. 
    * Check if all closed pull requests were properly tagged with the milestone.

### Open PRs

1. Review the open PRs.
2. If any of them seem like they should be merged (such as they are approved but not merged), check with the owner or team to see if it can be merged. Make sure to also tag them with the milestone if not already.
3. If an open PRs are tied to the milestone for this release and you are not going to merge them, move them to the next milestone.

### Closed PRs

1. Look at the recently closed PRs (note that GitHub displays them in the order they were created not in the order they were merged), and see if any public changes are missing a milestone. If so, add the correct milestone.

# Build and Test Code

### Checkout code

1. If you haven't already, clone the vmware/clarity repository (leave it as the origin) and we recommend to use this repo only for releasing. `git clone --depth 1 git@github.com:vmware/clarity.git release`
2. You'll want to always sync the latest code from the *master* branch. `git pull`
3. Make sure you get the latest node modules. `npm install`
4. Start the local server to preview the dev app. `ng serve`

### Review changes

1. Review the PRs for the milestone and verify that the changes appear to be working as expected for each.
2. Keep track of the features and write up release notes for each as you go (helps for later when doing website notes).
3. If anything seems out of place, review with the author or team before continuing with the release.

### Run tests

1. Verify that the tests are passing. `npm run test:travis`
2. Review the latest build on Travis for *master* to see if everything passes.

### Add release information

1. Update the version number in the *package.json* and *package-lock.json* files.
2. Update the release notes for the website, see https://github.com/vmware/clarity/wiki/Building-the-Website#adding-a-new-release.
3. Preview the website and release notes locally. `npm run website:start`
4. Generate markdown changelog file by running `npm run changelog`

### Build and commit

1. Build the packages. `npm run build`
2. Commit the changes to the *master* branch. `git commit -s -S -m 'release v1.0.0'`
3. Tag the commit with the version. `git tag v1.0.0`
4. Push the commit branch and tag (you must activate temporary admin rights first at https://github.vmware.com/admin). `git push origin master v1.0.0`

# Publish packages

1. Determine which publish script to run, there is *latest* when you are publishing the current version, and *next* when you are publishing a prerelease, and other scripts for old LTS versions.
2. Run publish to NPM. If it is the latest release use `npm run publish:latest`, if it is a prerelease use `npm run publish:next`.
3. Check if the packages appear on NPM, and that you get a confirmation email about the publishing. It may take a few minutes to appear.
4. Announce the release where appropriate.

# Update Icons

If new icons or updates to existing icons were made:
1. Clone the [Clarity Assets](https://github.com/vmware/clarity-assets) repo.
2. After building the main [Clarity project](https://github.com/vmware/clarity), unzip the icon folder the new icon is located in `/dist/clr-icons/shapes/`.
3. Copy any new icons to the appropriate icons folder in the [Clarity Assets](https://github.com/vmware/clarity-assets) repo.
4. Commit and push the updated icons to master.
