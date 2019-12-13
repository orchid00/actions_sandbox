
# Getting started with GitHub Actions

The goal of CIsandbox is to test some github actions with R. 

## What are GitHub actions?

GitHub actions allow us to trigger automated steps after we launch GitHub interactions such as when we push, pull, submit a pull request, or write an issue. 

Some example actions that we can implement:

- replace [Travis](travis.com) for continuous integration (CI)
- trigger automated messages every time a new issue is written or a pull request is initiated
- check if you code works of different OS

## Quick start

GitHub actions follow the steps designated in a `yaml` file, which is located in the `.github/workflows` folder of your repo.  

### The non-programatic way 

Go to any repo you _own_ and you will find "Actions" on the top menu. 
Click on "New Workflow" and pick one from the templates provided.
You can modify the `yaml` to adapt the action, such as the message.

### The more programatic way

In `R` @jimhester is working to add github action functionalities to the development version of the [`usethis` package](https://usethis.r-lib.org/reference/github_actions.html), which is a grand start! A few actions have specific `usethis` functions associated with them, for example those associated with continuous integration. We step through these in the following RMarkdown file: 

- set up continuous integration [here](https://github.com/ropenscilabs/CIsandbox/blob/master/docs/package-ci.Rmd)
- set up continuous integration with a reproducible environment using `renv` [here](https://github.com/ropenscilabs/CIsandbox/blob/master/docs/testing_with_renv.Rmd)

You can also access other actions that not only automate GitHub processess but provide programming-language-specific options at the GitHub [Marketplace](https://github.com/marketplace?type=actions). We demonstrate using some of these in other actions in the following RMarkdown files:



## More information and useful links

- R specific GitHub actions [examples](https://github.com/r-lib/actions/tree/master/examples) from r-lib
- `use_github_action` function and similar functions help [documentation](https://usethis.r-lib.org/reference/github_actions.html?q=#arguments) 
- [Glossary of actions](https://help.github.com/en/actions/automating-your-workflow-with-github-actions/core-concepts-for-github-actions)
- [Workflow syntax for GitHub Actions](https://help.github.com/en/actions/automating-your-workflow-with-github-actions/workflow-syntax-for-github-actions)

:tada: 
Now you know that are GitHub actions, and where to find more information about those!

---

Note: the [r-lib/ghactions](https://github.com/r-lib/ghactions) repo is deprecated!


### Meet the team members

* Chris
* David Neuzerling
* Murray
* Paula A Martinez
* Rhydwyn
* Saras Windecker

![team](https://twitter.com/WeAreRLadies/status/1205083457329565698/photo/1)
