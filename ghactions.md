## What are GitHub actions?

GitHub actions are a cool way to trigger actions for you, that would automate some part of your process.
For example, an action can be a message every time a new issue comes up:

Actions follow the steps on a `yaml` file 

You can find the yaml code for issue messages here:
https://github.com/ropenscilabs/CIsandbox/blob/master/.github/workflows/issuesmessage.yaml

Note: this and other examples are on the Github actions repo: 
[https://github.com/actions/github](https://github.com/actions/github)

The parts that were tricky to understand:

`on` can be `issues`, `pull`, `pull_request` you can use one or many as `[pull, pull_request]`
`uses`: `actions/checkout@master` or for the first ``

Note: the full documentation can be found here:
[https://help.github.com/en/actions/automating-your-workflow-with-github-actions/workflow-syntax-for-github-actions](https://help.github.com/en/actions/automating-your-workflow-with-github-actions/workflow-syntax-for-github-actions)

### R and GitHub actions

Note: R github actions examples can be found here:
[https://github.com/r-lib/actions/tree/master/examples](https://github.com/r-lib/actions/tree/master/examples)

https://usethis.r-lib.org/reference/github_actions.html?q=#arguments

