
# So what's actually going on in the yaml file? {#understanding-yaml}




Note: you can use `.yml` or `.yaml` as extension of your file for your workflow. 

Let's explore the `yaml` code for the first issue message here:

<details><summary>click me code</summary>
  <p>

        name: Greetings

        on: [pull_request, issues]

        jobs:
          greeting:
            runs-on: ubuntu-latest
            steps:
            - uses: actions/first-interaction@v1
              with:
                repo-token: ${{ secrets.GITHUB_TOKEN }}
                issue-message: 'Hi ! there!! thanks for your contribution!, you are awesome! '
                pr-message: 'Hey what an input! please give us a bit of time to review it! We will be in touch soon.'
  </p>
</details>

or here [https://github.com/ropenscilabs/CIsandbox/blob/master/.github/workflows/greetings.yml](https://github.com/ropenscilabs/CIsandbox/blob/master/.github/workflows/greetings.yml).

Translated that says,  the workflow action **name** is 'Greetings' is triggered on pull requests and issues. It will start a job
with the name greeting, and will run on a [runner](https://help.github.com/en/actions/automating-your-workflow-with-github-actions/core-concepts-for-github-actions#runner) for the example it is called ubuntu-latest. Then, each job has [steps](https://help.github.com/en/actions/automating-your-workflow-with-github-actions/core-concepts-for-github-actions#step) that will set up the environment in the runner with a few options. See more about the [syntax](https://help.github.com/en/actions/automating-your-workflow-with-github-actions/workflow-syntax-for-github-actions).

A few examples:

    `on` can be `issues`, `pull`, `pull_request` you can use one or many as `[pull, pull_request]`

    `uses`: `actions/checkout@master` or for the first `actions/first-interaction@v1`

## R Syntax options

Change the \<customise bits>

```
on:
  push:

name: <nameyouraction>

jobs:
  render:
    name: <nameyourjob>
    runs-on: macOS-latest
    steps:
      - uses: actions/checkout@v1
      - uses: r-lib/actions/setup-r@v1
      - uses: r-lib/actions/setup-pandoc@v1
      - name: <namestep1>
        run: Rscript -e 'install.packages("<the package you need>")'
      - name: <namestep2>
        run: Rscript -e 'rmarkdown::render("examples/README.Rmd")'
      - name: <namestep3>
        run: |
          git commit <some file>.md -m 'Re-build <file>.Rmd' || echo "No changes to commit"
          git push https://${{github.actor}}:${{secrets.GITHUB_TOKEN}}@github.com/${{github.repository}}.git HEAD:${{ github.ref }} || echo "No changes to commit"
```

* The `on` parameter tells GitHub what should trigger this action. In this case, we want to check code whenever it is pushed, or on a pull request. The latter is particularly useful because if we're about to merge code into the master branch, we want it to pass tests!
* The `name` of the action should be something that helps us identify at a glance what the action is doing. This is shown on github.com in the Actions tab of the repository.
* `runs-on` tells GitHub what sort of environment should run the job. These environments are called "runners". GitHub supports Ubuntu, macOS and Windows Server, as well as support for self-hosted runners.
* `uses` allows us to run other actions as part of our action. In this case, we're calling on actions that are defined in other repositories. The first action checks out the contents of our repository, and then next sets up R.
* The remaining steps are the commands we want to run as part of our action, each with a name. Here we're installing the dependencies of our package, as well as the `rcmdcheck` package we use to check the package in our repository. Finally, we're executing the command that checks the package.
