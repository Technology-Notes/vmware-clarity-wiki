# ks-app
The ks-app is a standard angular-cli app. It uses the compiled output of clarity to build and serve with. I'm using surge.sh to publish to for now. If you need/want to publish to the current location [http://clarity-ks.surge.sh](http://clarity-ks.surge.sh) let me know so I can add your surge.sh email. 

### Notes
 - Route pages / components are currently in a folder called `containers`. I almost called this folder `pages` but stuck with `containers`. I'm not really tied to either so if there is a strong preference for the other or something else I am happy to change it
- Adds demos for ks-app app, routing for component pages as an angular-cli app
- Adds ability to publish to surge.sh `npm run ks:publish`
- Keeps sample app for aot testing
- closes #1314 

### Getting ready
We use the latest artifacts from the clarity build process to develop and build the app for production. 
1. From the root of the clarity source you need to run `npm run prepublish:all`
2. From the root of the ks-app code (`clarity-src/src/ks-app`) you need to run `npm install`

### Development
The development server uses the webpack-dev-server (underlying the angular-cli tool) for development. To run it with the latest clarity artifact use these commands:
- `ng serve --preserve-symlinks`
- `ng serve --preserve-symlinks --prod`

### Build (prod)
The following command will bundle the latest Clarity artifact and generate a production ready (aot compiled) app in the `clarity-src/dist/ks-app` folder. 
- `ng build --preserve-symlinks --prod`

### Publish
If you have the getting ready steps complete, you can publish to surge.sh with the following command:
- `npm run ks:publish`

## Future enhancements

1. Reconfigure / setup a custom webpack config so that we can link, consume and generate source-maps for the Clarity source files for a better development experience. 
2. Add testing for the containers and components
3. Polish with route animations
