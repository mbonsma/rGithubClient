## rGithubClient
##### Making it easier for R to talk to GitHub

-----

##### Installing the `rGithubClient`:

Currently, the `rGithubClient` is not available via CRAN, but can be install directly from GitHub using the `devtools` package:

```r
install.packages("devtools")
require(devtools)
install_github("brian-bot/rGithubClient")
```

-----

##### Overview

purpose is to allow users to:
* use github as a version control system for analysis code in addition to enterprise software development
* store code centrally for sourcing into an analysis environment
* allow easy sharing and forking of code that may be useful for others

current status:
* For access to private repositories and/or to have an increased limit on the number of API calls, users should register a personal access token with the client via the `setGithubToken` function. Personal access tokens can be generated on your [GitHub settings page](https://github.com/settings/applications). Once you have called `setGithubToken`, the token passed to this function is then used for all subsequent calls to github api for the current R session.
* currently staying away from downloading files -- sticking with meta-information and ability to directly source files
* `sourceRepoFile` sources code into the global environment, but allows users to pass optional arguments as specified in the `base::source()` function

-----

##### Quickstart Guide

```r
## LOAD THE PACKAGE
require(rGithubClient)

## USE TOKEN TO AUTHENTICATE FOR YOUR CURRENT SESSION
setGithubToken("myTokenFromGithub12345678")

#####
## ACCESSING META-INFORMATION ABOUT A GITHUB REPOSITORY
#####
## FOR HEAD OF MASTER BRANCH OF A GITHUB REPOSITORY
repoHead <- getRepo('brian-bot/rGithubClient')

## OR HEAD OF A SPECIFIC BRANCH (dev)
repoBranch <- getRepo('brian-bot/rGithubClient', ref='branch', refName='dev')

## OR A SPECIFIC TAG
repoTag <- getRepo('brian-bot/rGithubClient', ref='tag', refName='rGithubClient-0.8')

## OR A SPECIFIC COMMIT
repoCommit <- getRepo('brian-bot/rGithubClient', ref='commit', refName='d3960fdbb8b1a4ef6990d90283d6ec474e424d5d')


#####
## VIEW THE SPECIFIC TIMEPOINT ON GITHUB WEBSITE
#####
view(repoHead)


#####
## SOURCING A FILE FROM A REPOSITORY
#####
sourceRepoFile(repoDev, "inst/demo/helloWorld.R")

```
