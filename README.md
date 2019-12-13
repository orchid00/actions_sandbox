
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

* Chris Brown
* Murray Cadzow
* Paula A Martinez
* Rhydwyn McGuire
* David Neuzerling
* David Wilkinson
* Saras Windecker

![team](https://twitter.com/WeAreRLadies/status/1205083457329565698/photo/1)
