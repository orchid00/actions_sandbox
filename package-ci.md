

# Example workflow to set up continuous integration for packages {#packageci}



This is an example workflow to create a package and use Github actions apply continuous integration to automatically check and test packages upon a git push.

Github actions are included in the dev version of `usethis` which can be installed from github using


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

### Existing package with github

Make sure that you have GitHub set up with your package.

[Existing project and package, github first](https://happygitwithr.com/existing-github-first.html#existing-github-first)
[Existing project and package, github last](https://happygitwithr.com/existing-github-last.html#existing-github-last)

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

This creates the required yaml file in `.github/workflows/` for using the GitHub action that runs the release-check for a package on gitGitHubhub and includes the code to add the badge in your readme.

Now git add, commit the changes and push them to your repo and the action will run! 



