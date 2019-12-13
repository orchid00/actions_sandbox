
# Getting started with GitHub actions

The goal of actions_sandbox is to explore some GitHub actions with R. 

## What are GitHub actions?

GitHub actions allow us to trigger automated steps after we launch GitHub interactions such as when we push, pull, submit a pull request, or write an issue. 

For example, there are actions that will automatically trigger:

- continuous integration (CI)
- messages in response to issues or pull requests
- rendering/compiling eg. of bookdown, blogdowns etc

GitHub actions follow the steps designated in a `yaml` file, which we place in the `.github/workflows` folder of the repo. 
We can add these `yaml` files to our repo either by clicking on a series of steps on GitHub.com, or using wrapper functions provided by the `usethis` package, depending on which actions you which to include.
We describe both ways here. 

### Meet the team members 

* 🤓 [Chris Brown](https://github.com/CStats) 🐦 [\@CStatsAU](https://twitter.com/CStatsAU)
* 🤓 [Murray Cadzow](https://github.com/murraycadzow) 🐦 [\@Rhydwyn McGuire](https://twitter.com/murraycadzow)
* 🤓 [Paula A Martinez](https://github.com/orchid00) 🐦 [\@orchid00](https://twitter.com/orchid00)
* 🤓 [Rhydwyn McGuire](https://github.com/rhydwyn) 🐦 [\@rhydwyn](https://twitter.com/rhydwyn)
* 🤓 [David Neuzerling](https://github.com/mdneuzerling) 🐦 [\@mdneuzerling](https://twitter.com/mdneuzerling)
* 🤓 [David Wilkinson](https://github.com/Doi90)
* 🤓 [Saras Windecker](https://github.com/smwindecker) 🐦 [\@smwindecker](https://twitter.com/smwindecker)

![team](team.jpeg)

## Meta

* Please [report any issues or bugs](https://github.com/ropenscilabs/CIsandbox/issues).
* License: MIT
* Please note that this project is released with a [Contributor Code of Conduct](CODE_OF_CONDUCT.md). By participating in this project you agree to abide by its terms.

[![rofooter](https://ropensci.org/public_images/github_footer.png)](https://ropensci.org)
