# R Development Collaboration Guide

## Rules

The following set of rules should be followed by all contributors and checked by
all reviewers of the OSPS R projects.

1. Each change made to the codebase should have a clear purpose and exist in an
isolated context.  
  1.1 Each change should be related to an issue created on the project's repository.  
  1.2 Each change should be made in a separate branch.  
  1.3 Each change should be proposed through a pull request.  
  
2. Each change or addition to the code should be documented and controlled.  
  2.1 Each change in the code should be reflected in the documentation. If 
  documentation is not present, then it should be created.  
  2.2 Each change should be tested. If new cases emerge, then they should be 
  tested, even if some tests are already present. If no tests are present, then
  they should be created.  
  
3. Each change should be easily reviewable, understandable and accessible.   
  3.1 Each change should have a corresponding entry in the `NEWS` file.  
  3.2 Each change should be associated with a pull request which scope is limited to the change itself.  
  
  
4. Each change must respect the coding style of the project.    
  4.1 Each change must respect the coding style of the project as defined in the [R Coding Standards](CODING_STANDARDS_R.md).  
  4.2 Each change must be processed by the `{styler}` package before being proposed.  
  
  
5. Each change should be reviewed before being merged.  
  5.1 Each change should be reviewed by at least one other contributor through its associated pull request.  
  5.2 Each change should be functional and comply with these rules before its associated pull request is set as "ready for review". If not ready or reviewer inputs are needed, the pull request should be marked as "draft".  
  
  


## Recommended Workflows

### Changing Code

The recommended workflow for contributing to the OSPS R projects heavily relies on the [`{usethis}`](https://usethis.r-lib.org) package and it family of function [`pr_*()`](https://usethis.r-lib.org/articles/pr-functions.html).

#### Prerequisites

This workflow implies that:

-   R and R Studio are installed,
-   A GitHub account is available and setup to work within RStudio,
-   The `{usethis}` package is installed,
-   A local clone (from original repository or from a fork) has been created.

#### Workflow

1.  Initialize `usethis::pr_init("my-branch-name")`.
2.  Apply changes in codebase and save with commits
3.  Once changes are implemented, make a pull request with `usethis::pr_push()`.
4.  Review of the pull request may ask for additional changes, proceed with commits then use the `pr_push()` command again.
5.  Finally, the reviewer merge the pull request, the local branch can be cleaned away using `usethis::pr_finish()`

#### Useful tips

-   At any moment you can get back to main branch using `usethis::pr_pause()`
-   If you need to make some changes on a branch that already has a pull request open, you can retrieve it locally with `usethis::pr_fetch(XX)` with `XX` being the pull request's numerical identifier.

<!--- ### Reviewing Code  --->


### Releasing Versions

**This section is only applicable for the following repositories:**
  - `{OSPSuite.ParameterIdentification}`
  - `{esqlabsR}`
  
#### Prerequisites

This workflow implies that:

- R and R Studio are installed,
- A GitHub account is available and setup to work within RStudio,
- The `{usethis}` package is installed,
- A local clone (from original repository or from a fork) has been created.
- The current branch is the default branch (usually `main`).

#### Workflow

The recommended workflow for contributing to the OSPS R projects heavily relies on the [`{usethis}`](https://usethis.r-lib.org) package.

1. Pick the new version number using the following command (refer to [this](https://r-pkgs.org/lifecycle.html#sec-lifecycle-version-number) to make the right choice).
```r
new_version <- usethis:::choose_version("What should the new version be?")
  ```
2. Create a dedicated branch
```r
usethis::pr_init(branch = paste("release", new_version, sep = "-"))
```
    
3. Automatically update version number and DESCRIPTION file
```r
usethis::use_version(which = labels(new_version))
```

4. Commit all changes

5. Create the pull request
```r
usethis::pr_push()
```

6. Once the pull request is approved and merged, the release is done. The local branch can be cleaned away using `usethis::pr_finish()`.

7. The package should be put back to development mode. 

Pick "dev" after executing the following code.

```r
new_version <- usethis:::choose_version("What should the new version be?")
```

8. Repeat steps 2 to 6.


