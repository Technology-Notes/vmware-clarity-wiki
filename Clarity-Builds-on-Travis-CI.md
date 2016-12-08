Clarity is built on [Travis](https://travis-ci.org/vmware/clarity) for every push, including pull requests. We require that every pull request passes the build on Travis before it can be merged into master. Travis executes three parallel jobs on a single build by using an environment variable called `TEST_SUITE` defined in our `.travis.yml` as follows:

```
env:
  global:
    - CXX=g++-4.8
  matrix:
    - TEST_SUITE=test
    - TEST_SUITE=css:test
    - TEST_SUITE=css:reference
```

Our script command will then run the jobs using the environment variable to run them in parallel:

```
script:
  - gulp $TEST_SUITE
```

We use [Jasmine](https://jasmine.github.io/) and [Karma](https://karma-runner.github.io/) for our unit tests. Our css regression tests are written with [Gemini](https://gemini-testing.github.io/).

Here's a more detailed description of what each job does:
* `TEST_SUITE=test`: builds Clarity in prod mode and runs the unit tests. This job does not produce any artifacts.
* `TEST_SUITE=css:test`: builds Clarity and runs the css regression tests. This job produces the following artifacts, which are uploaded to s3:
   * **html report from the css regression test**: The actual download url is produced at runtime and can be found towards the bottom of the console log from the job. The url will typically end in `../clarity/gemini-report/index.html`. Here is an example snippet from a job's console log:
   ```
   INFO: uploading: /home/travis/build/jeeyun/clarity/gemini-report/index.html (size: 464KB)
	  download_url: https://s3.amazonaws.com/travis-ci-jeeyun/jeeyun/clarity/105/105.2/home/travis/build/jeeyun/clarity/gemini-report/index.html
   ```
   * **selenium log file**: This is only useful if the css tests failed to run due to selenium issues and will typically end in `../selenium.txt`. Here is an example snippet from a job's console log:
   ```
   INFO: uploading: /home/travis/build/jeeyun/clarity/selenium.txt (size: 2.7MB)
	  download_url: https://s3.amazonaws.com/travis-ci-jeeyun/jeeyun/clarity/105/105.2/selenium.txt
   ```
* `TEST_SUITE=css:reference`: builds Clarity and takes screenshots of every component that's tested in the css regression test **from the current build's code**. This is useful because if a css regression test fails due to an expected visual change, then you can download the new set of screenshots, and replace the current (which are located in `gemini/screens` directory from Clarity project's root, and check them in to your PR branch. The subsequent build should hopefully pass! If the visual changes require change in tests, then you can add or edit existing tests under `gemini/tests` directory from Clarity project's root.
   * **reference screenshots**: The entire set of screenshots is zipped and uploaded to s3 and will have a url that ends in `../screenshots.zip`. Here is an example snippet from a job's console log:
   ```
   INFO: uploading: /home/travis/build/jeeyun/clarity/screenshots.zip (size: 2.6MB)
  download_url: https://s3.amazonaws.com/travis-ci-jeeyun/jeeyun/clarity/105/105.3/screenshots.zip
   ```
   * **selenium log file**: This is only useful if the job failed to run due to selenium issues and will typically end in `../selenium.txt`.
