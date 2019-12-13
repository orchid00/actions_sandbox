

# Example workflow to set up continuous integration for packages {#packageci}



This is an example workflow to create a package and use Github actions apply continuous integration to automatically check and test packages upon a git push.

Github actions are included in the dev version of `usethis` which can be installed from Github using


```r
# install.packages("devtools")
devtools::install_github("r-lib/usethis")
```

## Package setup and connect with Github

### New project, Github first

Follow instructions for setting up a new project with [happygitwithr](https://happygitwithr.com/new-github-first.html#new-github-first)

Create a package

```r
usethis::create_package(path = "path-to-project")
```

### Existing package with Github

Make sure that you have Git Hub set up with your package. Refer to https://happygitwithr.com/ for setting up with an existing project.

- [Existing project and package, github first](https://happygitwithr.com/existing-github-first.html#existing-github-first)

- [Existing project and package, github last](https://happygitwithr.com/existing-github-last.html#existing-github-last)

### Add Github links to DESCRIPTION

Before initiating GitHub actions, you'll need to point to where your GitHub instance is located. The following function populates the URL and BugReports fields of a GitHub-using R package DESCRIPTION file with links to GitHub. If your project is hosted by an enterprise GitHub server you'll need to modify the input arguments. 


```r
usethis::use_github_links()
```

## Actions for continuous integration checks

### release-check

This option checks your work using 

```r
usethis::use_github_actions()
```

This creates the required yaml file in `.github/workflows/` for using the GitHub action that runs the release-check for a package on GitHub and includes the code to add the badge in your README.

Now git add, commit the changes and push them to your repo and the action will run! 



