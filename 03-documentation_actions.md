# Websites using pkgdown, bookdown, and blogdown



## Create gh-pages branch {#ghpages-setup}

In order to serve html pages through GitHub pages the following needs to be done to create an emtpy gh-pages branch to be used to deploy the html pages created by either `pkgdown`, `bookdown`, or `blogdown`

Derived from: https://pkgdown.r-lib.org/reference/deploy_site_github.html

First we need to create an empty gh-pages branch. In bash:
  
```
git checkout --orphan gh-pages
git rm -rf .
git commit --allow-empty -m 'Initial gh-pages commit'
git push origin gh-pages
git checkout master
```

## Action to deploy a pkgdown site

To add auto-generating website documentation for a package, we can leverage off `pkgdown` and add it to an existing package, and then use a GitHub action to auto generate the docuemtation and deploy it to a GitHub pages site.

First we add the use of `pkgdown` to the package:


```r
usethis::use_pkgdown()
```

Then we want to add in the github action for pkgdown to automatically add documentation. There is an existing yaml template example in the `actions` package:


```r
usethis:::use_github_action(url = "https://raw.githubusercontent.com/r-lib/actions/master/examples/pkgdown.yaml")
```

The yaml file should be located in .github/workflows/pkgdown.yml and looks like:
```
on:
  push:
    branches: master

name: Pkgdown

jobs:
  pkgdown:
    runs-on: macOS-latest
    steps:
      - uses: actions/checkout@master
      - uses: r-lib/actions/setup-r@master
      - uses: r-lib/actions/setup-pandoc@master
      - name: Install dependencies
        run: |
          Rscript -e 'install.packages("remotes")' \
                  -e 'remotes::install_deps(dependencies = TRUE)' \
                  -e 'remotes::install_github("jimhester/pkgdown@github-actions-deploy")'
      - name: Install package
        run: R CMD INSTALL .
      - name: Deploy package
        run: |
          Rscript -e "pkgdown:::deploy_local(new_process = FALSE, remote_url = 'https://x-access-token:${{secrets.GITHUB_TOKEN}}@github.com/${{github.repository}}.git')"
```

N.B. The usethis function is not currently exported into the NAMESPACE of `usethis` but is documented.

Now we need to git add and commit the yaml file, and push the changes to Github.

## Action to deploy a bookdown site

The following yaml template will run `bookdown::render_book()` on index.Rmd and then deploy the resulting html files onto the gh-pages branch that was created as part of section \@ref(ghpages-setup). It also requires the creation of two GitHub secrets (see section \@ref(secrets)), _GITHUB_PAT_ and _EMAIL_. _GITHUB_PAT_ is a personal access token that has at least repo access, create the token in your personal settings and then copy the value into the secrets settings for the repository (see section \@ref(github-pat) for more). The action also assumes that you are compiling the book to an html format and the output directory is `_book`.

Github action for .github/workflow/deploy_bookdown.yml
```
on:
  push:
     branches:
       - master
  pull_request:
     branches:
       - master
  

name: renderbook

jobs:
  bookdown:
    name: Render-Book
    runs-on: macOS-latest
    steps:
      - uses: actions/checkout@v1
      - uses: r-lib/actions/setup-r@v1
      - uses: r-lib/actions/setup-pandoc@v1
      - name: Install rmarkdown
        run: Rscript -e 'install.packages(c("rmarkdown","bookdown"))'
      - name: Render Book
        run: Rscript -e 'bookdown::render_book("index.Rmd")'
      - uses: actions/upload-artifact@v1
        with:
          name: _book
          path: _book/
  
# Need to first create an empty gh-pages branch
# see https://pkgdown.r-lib.org/reference/deploy_site_github.html
# and also add secrets for a GITHUB_PAT and EMAIL to the repository
# gh-action from Cecilapp/GitHub-Pages-deploy
  checkout-and-deploy:
   runs-on: ubuntu-latest
   needs: bookdown
   steps:
     - name: Checkout
       uses: actions/checkout@master
     - name: Download artifact
       uses: actions/download-artifact@v1.0.0
       with:
         # Artifact name
         name: _book # optional
         # Destination path
         path: _book # optional
     - name: Deploy to GitHub Pages
       uses: Cecilapp/GitHub-Pages-deploy@master
       env:
          EMAIL: ${{ secrets.EMAIL }}               # must be a verified email
          GH_TOKEN: ${{ secrets.GITHUB_PAT }} # https://github.com/settings/tokens
          BUILD_DIR: _book/                     # "_site/" by default
    
``` 
This action is performed using two jobs, the first renders html, and the second deploys the html to the gh-pages branch so that it can be viewed using the url \<user/org_name>.github.io/\<repository_name>. It achieves this by passing an artifact (the `_book` directory) between jobs. Further information about the action yaml files can be found in chapter \@ref(understanding-yaml).

To use the above yaml file that is responsible for deploying this book, you can add it to your book using `usethis`

```r
usethis:::use_github_action(url = "https://raw.githubusercontent.com/ropenscilabs/actions_sandbox/master/.github/workflows/deploy_bookdown.yml")
```

N.B. `usethis:::use_github_action()` is not currently exported into the NAMESPACE of `usethis`.

