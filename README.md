# Revisting the [Research Compendium](https://github.com/ropensci/rrrpkg)

Lessons from package development for the creation of reproducible analyses.

## 1. A testing framework

-  Separate testing code analysis or presentation code
   - Use packages such as assertr, validate
   - Statistical inspection plots
-  Testing for analyses should test *objects* not lines of code
-  All objects created in the environment of an R markdown file or script
   should be available for testing
-  Types of tests:
   -  By type of object
      -  Data tests: both raw data and processed data objects have expected properties
      -  Model tests: models have expected properties
      -  Value tests: derived quantities within reasonable bounds
  -  By output
      -  Boolean tests: easily defined as errors
      -  Visual or output tests: Printed or plotted outputs must be inspected.
-   Test *coverage* means that objects have been inspected, possibly by how
    much they have been inspected
-   Tests compiled into single HTML report or structured list/JSON
-   Running `test()` should result in pop-up of the test report or object.

## 2. A build framework

-   `make` or **remake** based.


## 3. A CI framework

-   The build framework is run, and changes are re-committed
-   Both outputs and tests must be easy to inspect in CI, so as to be able to judge
    and merge them.
-   Must deal with computationally-intensive issues
    - Cache knitr/remake objects in the CI
    - Deal with file modified times for git.

## 3. A review framework

-   Of course this will be overly general, but checklists help! Must start somewhere
-   Model assumptions are met
-   Data is reasonable
-   Graphics represent the information well
-   Guards against overfitting, p-hacking, etc.

## Easy set-up and migration

A **projtools** package to support the above workflows.

-  `setup()` for **ProjectTemplate**-like directory arrangements
-  `use_docker()` to quickly generate at Dockerfile with current R version
-  `use_packrat()` to quickly set up packrat with existing packages
-  `use_ci()` to get your `.travis.yml()`, etc. files going
-  `bootstrap()` everything at once.
-  `run()` to compile the project and run tests without repeating.
-  `inspect()` to wrap any printed or plotted outputs
-  `expect()`  to test any boolean or similar **testthat**-like condition

## For open's sake, closed and private workflows first!

-  Users have to be able to test, share, and CI privately and within trusted
   groups before sharing broadly
-  Training and documentation have to assume a private workflow as the *primary* use-case.
-  Robust private workflows are easily switched to public, but if public is forced,
   many users will never get there.
