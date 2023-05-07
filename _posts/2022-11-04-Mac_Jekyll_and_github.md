---
title: Getting Jekyll Working
by: Stuart Hirst
date: 2022-11-4 12:00:00
categories: [hosting,web]
tags: [youtube,misc]
pin: true
---

# Tips & Tricks to getting Jekyll working

NOTE: This needs updating with new Github "Pages" options. 

## Overview

Whilst setting up our YouTube channel [How Hard Can It Be](https://www.youtube.com/@howhardcanitbe-live) and the linked services, we decided to create a supporting documentation site to capture project details. We followed posts from [Techno Tim](https://youtu.be/F8iOU1ci19Q) which were great but didn't quite work for us. I recommend you follow and subscribe to to [Tim's channel](https://www.youtube.com/c/TechnoTimLive), he has some great content and clear details to get things working.

 Here we share what we found and what worked for us:

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
The original attempts to compile failed due to SSL errors so to work around the issues we used a specific set of libraries which are set using the environment variables below. We had two versions of SSL "openssl@1.1" and "openssl@3" which was the default. By using "openssl@1.1" we managed to get Jekyll to compile. 

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

# Summary

Hopefully everything worked and your Jekyll site compiled correctly. If you have issues, the compile logs are very verbose and that combined with lots of Googling eventually solved our issues. I hope this helps someone else and saves you a little time.




