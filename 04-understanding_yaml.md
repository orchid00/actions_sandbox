
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
                repo-token: ${{ secrets.GH_TOKEN }}
                issue-message: 'Hi ! there!! thanks for your contribution!, you are awesome! '
                pr-message: 'Hey what an input! please give us a bit of time to review it! We will be in touch soon.'
  </p>
</details>

or here [https://github.com/ropenscilabs/CIsandbox/blob/master/.github/workflows/greetings.yml](https://github.com/ropenscilabs/CIsandbox/blob/master/.github/workflows/greetings.yml).

Translated, that says that the workflow action **name** is 'Greetings' and is triggered on pull requests and issues. It will start a job
with the name _greeting_, and will run on a [runner](https://help.github.com/en/actions/automating-your-workflow-with-github-actions/core-concepts-for-github-actions#runner) called _ubuntu-latest_. Then, each job has [steps](https://help.github.com/en/actions/automating-your-workflow-with-github-actions/core-concepts-for-github-actions#step) (here there is only one) that will pass commands to the runner or call externally-defined actions, possibly passing parameter values to those actions or setting up the environment by defining environment variables. See more about the [syntax](https://help.github.com/en/actions/automating-your-workflow-with-github-actions/workflow-syntax-for-github-actions).

## GitHub action options

Change the \<customizable bits> as needed:

```
on:
  push:
  pull-request:

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
          git push https://${{github.actor}}:${{secrets.GH_TOKEN}}@github.com/${{github.repository}}.git HEAD:${{ github.ref }} || echo "No changes to commit"
```

* The `on` parameter tells GitHub what should trigger this action. In this case, we want to check code whenever it is pushed, or on a pull request. The latter is particularly useful in the case of a CI action because if we're about to merge code into the master branch, we want it to pass the tests!
* The `name` of the action should be something that helps us identify at a glance what the action is doing. This is shown on github.com in the Actions tab of the repository.
* `runs-on` tells GitHub what sort of environment should run the job. These environments are called "runners". GitHub supports Ubuntu, macOS and Windows Server, as well as self-hosted runners.
* `uses` allows us to run other actions as part of our action. In this case, we're calling on actions that are defined in other repositories. The first action checks out the contents of our repository; the second and third then set up R and Pandoc.
* The remaining steps, each with a name, contain the commands we want to run as part of our action. Here we're installing the dependencies of our package.  (In the R-CMD-check action produced by `usethis::use_github_action_check_release()` (see section 2.2.1), we install the `rcmdcheck` package as well—it's what we use to check the package in our repository—and then we go ahead and do the check by calling the package-checking function it provides.)


## GitHub Secrets {#secrets}

[GitHub secrets](https://help.github.com/en/actions/automating-your-workflow-with-github-actions/creating-and-using-encrypted-secrets) are a way to use values in your yaml that need to remain secret, such as credentials or information you want to keep private. Commonly this would be a [GitHub personal access token](https://help.github.com/en/github/authenticating-to-github/creating-a-personal-access-token-for-the-command-line) (_GH_PAT_) that enables the action to perform operations such as _push_. These are set under the repository settings menu.

![](images/add_secret.png)<!-- -->



### Personal access tokens {#github-pat}

Personal access tokens can be generated with differing levels of authority. To create one for your account, go to https://github.com/settings/tokens and click "Generate new token". Then you can copy the value of the token into a secret for your repository so that a GitHub action can be authenticated as you.
