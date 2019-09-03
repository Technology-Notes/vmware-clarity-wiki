## About
CSS regression is run with a suite of gemini tests. In order to make testing easy in a variety of environments we added support for running our suite inside a Docker container.

Running tests locally depends on having [Docker](https://www.docker.com/get-docker) installed and running. 

We also need `gemini` and the `html-reporter` installed on the local machine.
- npm install -g gemini
- npm install -g html-reporter

There are two commands built into our npm scripts:

1. Run tests
    1. `npm run  test:visual:light set1` will run all the test suites in set1 for the light theme
    2. `npm run  test:visual:light set1/buttons.js` will run the buttons.js suite of tests for the light theme
2. Update reference images
    1. `npm run visual:fix:light set1` will run `gemini update` on all the test suites in set1 for the light theme
    2. `npm run visual:fix:light set1/buttons.js` will run `gemini update` on the buttons.js test suite for the light theme


Note: we have currently broken up the tests into two sets, set1 and set2. 

## References
1. [What is Docker?](https://www.docker.com/what-docker)
2. [What is Gemini?](https://github.com/gemini-testing/gemini)
3. [What is Selenium?](http://www.seleniumhq.org/)