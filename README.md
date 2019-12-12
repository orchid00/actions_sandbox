
# Getting started with GitHub Actions

<!-- badges: start -->
<!-- badges: end -->

The goal of CIsandbox is to test some github actions with R and secrets

ghactions deprecated [ghactions](https://github.com/r-lib/ghactions)
usethis actions pulls workflows from examples directory. 
downloads the check release yaml file and puts in your repo
it feeds from the actions examples. helper functions. 



Team members: test some github actions with R and secrets

* Saras
* Chris
* David
* Murray
* Paula
* Rhydwyn

explore usage of github actions with an r package

- [ ] simple package
- [ ] github action for check
- [ ] github action


What are GitHub actions? 


What kind of actions can you implement?
See the [marketplace](https://github.com/marketplace?type=actions) for all the already available yaml options. 

How do I implement a GitHub action? 
You can do so by point and click on GitHub by: 

You can do so using helper wrapper

How to add a secret!
copy the token. go to settings, secrets, add new secret. 

usethis::use_github_action()

Getting it set up is really straightforward
No extra authentication
Jim is migrating!

It works with test coverage as well. 
Go to codecov for repo, settings, copy repo token, put it in your actions settings as a secret. 
check_full for all three OSs.

cross compatibility unlikley a problem if your package is mostly r code. so checking just with check_release likely sufficient. 

?secret for use in code. 
?
