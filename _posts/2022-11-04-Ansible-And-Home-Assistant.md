---
title: Ansible and Home Assistant
by: Stuart Hirst
date: 2022-11-15 12:00:00
categories: [hosting,web]
tags: [youtube,misc]
pin: true
---

# Ansible and Home Assistant

## Overview

One of our recent projects is to make our home more resilient. We installed UPS systems for critical services, install power bypass to enable powering the entire home from a generator and installing a backup 5G modem and antenna. All of this means that if the power goes out or if NBN(Internet) fails, the house automatically fails over to backup services and lets us know.

This is a related project to automation it infrastructure actions based on resilience events. The general plan is that Home Assistant will detect events and trigger automations executed by Ansible to manage systems and servers enabling a controlled response to resilience issues. For example, shutting down non-critical systems whilst on UPS power.

## References

 * [Techno Tim](https://youtu.be/F8iOU1ci19Q) 

## Related Projects

Companion projects are listed below and where the documentation is ready, its linked for easy access. If its not linked then the documentation for that project isn't quite ready yet:

* UPS Install and Home Assistant Integration
* Internet Resilience and 5G Install
* Generator Backup 


## Our Setup















.





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




