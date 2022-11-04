---
title: Getting Jekyll Working
by: Stuart Hirst
date: 2022-11-4 12:00:00
categories: [hosting,web]
tags: [youtube,misc]
pin: true
---

# Tips & Tricks to getting Jekyll working

## Overview

Whilst setting up our channel and the linked services, we decided to create a supporting documentation site to capture project details. We followed posts from "Techno Tim" which we great but didnt quite work for us. Here we share what we found and what worked for us.

## Our Setup

We use a few Mac's, both Intel and M1 to develop and write content. Github is our preferred GIT provider and we need to be able to update and create content dynamically. We like the Chirpy Jekyll theme and need an easy to maintain process for updates and new posts.

## Working Versions

```shell
$ ruby -v
ruby 3.0.0p0 (2020-12-25 revision 95aff21468) [arm64-darwin21]

$ bundle --version
Bundler version 2.3.24

$ brew --version
Homebrew 3.6.7
Homebrew/homebrew-core (git revision 3768ae96c6f; last commit 2022-10-31)
Homebrew/homebrew-cask (git revision f11b87600d; last commit 2022-10-31)
```

# Issues & Workarounds

## Installing Ruby

The default install mechanism for Ruby didn't "just work" when trying to install on the Mac M1 machine. What worked for us was:

```shell
brew install ruby@3.0
```

Install openssl and setup the environment variables:

```shell
brew install openssl
```
Set the environment variables to the following in either ~/.zshrc or ~/.bash:

```shell
LDFLAGS=-L/opt/homebrew/opt/openssl@1.1/lib
CPPFLAGS=-I/opt/homebrew/opt/openssl@1.1/include
PKG_CONFIG_PATH=/opt/homebrew/opt/openssl@1.1/lib/pkgconfig
```
## Compiling Jekyll with SSL

```shell
arch -arm64 gem install --user-install bundler jekyll
```






