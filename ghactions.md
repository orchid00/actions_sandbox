## What are GitHub actions?

GitHub actions are a cool way to trigger actions for you in an automated way, to help with any of your processes on your github repos.
For example, an action can be a message every time a new issue comes up.

GitHub actions follow the steps on a `yaml` file, which is usually located on the `.github/workflows` folder of your repo. You can find the `yaml` code for issue messages here:
https://github.com/ropenscilabs/CIsandbox/blob/master/.github/workflows/issuesmessage.yaml

<details><summary>click me code</summary>
  <p>


        name: Triage
        on:
          issues:
            types: [opened]
        jobs:
          commentOnNewIssues:
            name: Comment On New Issues
            runs-on: ubuntu-latest
            steps:
              - uses: actions/checkout@master
              - name: Comment On New Issues
                uses: actions/github@v1.0.0
                env:
                  GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
                with:
                  args: comment "Thanks for your issue! we are going to work on that"

  </p>
</details>

Note: this and other examples are located on the Github actions repo: 
[https://github.com/actions/github](https://github.com/actions/github)
which serve as the actions-toolkit for common _GitHub automations_. 

If you feel like finding _more actions_, that will help not only automating GitHub processess but programming-language-specific actions, you can dive into the Github Marketplace
[https://github.com/marketplace?type=actions](https://github.com/marketplace?type=actions)
which will point you to thousands of actions provided by the community.

:tada: 
Now you know that are GitHub actions, and where to find more information about those!

## How to create new GitHub actions?

### The non-programatic way 

Go to any repo you _own_ and you will find the "Actions" menu. 
Click on New workflow and pick one form the templates provided.
You can modify the `yaml` to adapt your needs.

To understand the parts of the `yaml` see below.

### The more programatic way

In `R` @jimhester is working to add github action functionalities to the `{usethis}` package here: [https://usethis.r-lib.org/reference/github_actions.html](https://usethis.r-lib.org/reference/github_actions.html) and that is a grand start!

We've learned: 
* Need to install the new (as of December 2019) in development version of `{usethis}` from GitHub
* Follow this awesome vignette:
[https://github.com/ropenscilabs/CIsandbox/blob/master/docs/package-ci.Rmd](https://github.com/ropenscilabs/CIsandbox/blob/master/docs/package-ci.Rmd)

Note: R github actions examples can be found here:
[https://github.com/r-lib/actions/tree/master/examples](https://github.com/r-lib/actions/tree/master/examples)

To start understanding the arguments here is a innitial help documentation for the `use_github_action(` function and similar functions 
[https://usethis.r-lib.org/reference/github_actions.html?q=#arguments](https://usethis.r-lib.org/reference/github_actions.html?q=#arguments).

### Understanding parts of the yaml file

The parts of the yaml file that were tricky to understand:

`on` can be `issues`, `pull`, `pull_request` you can use one or many as `[pull, pull_request]`

`uses`: `actions/checkout@master` or for the first `actions/first-interaction@v1`

Note: the full documentation can be found here:
[https://help.github.com/en/actions/automating-your-workflow-with-github-actions/workflow-syntax-for-github-actions](https://help.github.com/en/actions/automating-your-workflow-with-github-actions/workflow-syntax-for-github-actions)

More on other nifty vignette: [https://github.com/ropenscilabs/CIsandbox/blob/master/github-actions-yaml-description.Rmd](https://github.com/ropenscilabs/CIsandbox/blob/master/github-actions-yaml-description.Rmd).

