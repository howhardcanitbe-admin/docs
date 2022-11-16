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

One of our recent projects was to make our home more resilient. We installed UPS systems for critical systems and services, install power bypass to enable powering the entire home from a generator and installing a backup 5G modem and antenna. All of this means that if the power goes out or if NBN(Internet) fails, the house automatically fails over to backup services and lets us know.

This is a related project to automation IT infrastructure actions based on resilience events. The general plan is that Home Assistant will detect events and trigger automations executed by Ansible to manage systems and servers enabling a controlled response to resilience issues. For example, shutting down non-critical systems whilst on UPS power.

## References & Links

* [How Hard Can It Be Youtube Channel](https://youtube.com/@howhardcanitbe-live)

 * [Techno Tim](https://youtu.be/F8iOU1ci19Q)
 * [Home Assistant](https://www.home-assistant.io/)
 * [Ansible](https://www.ansible.com/)
    * [Installing Ansible on Raspberry Pi](https://www.theurbanpenguin.com/installing-ansible-on-the-raspberry-pi/)
 * [Ansible AWX](https://www.ansible.com/community/awx-project)

## Related Projects

Companion projects are listed below and where the documentation is ready, its linked for easy access. If its not linked then the documentation for that project isn't quite ready yet:

* UPS Install and Home Assistant Integration
* Internet Resilience and 5G Install
* Generator Backup 


## Our Setup

Ansible is installed on a Raspberry PI used as the Pi-Hole DNS Server. Ansible has its own GIT repo and so its easy to move in the future. In the future we will be deploying a resilient Proxmox cluster and Ansible will eventually reside there.

We also plan to use [Ansible AWX](https://www.ansible.com/community/awx-project) to provide a GUI and management framework for Ansible. This also provides an API that Home Assistant can use to trigger Ansible playbooks.

## Installing Everything

### Ansible

These are the commands used on the Raspberry PI to install Ansible:


1) Add the Ansible repo
```shell
sudo echo "deb http://ppa.launchpad.net/ansible/ansible/ubuntu trusty main" >> /etc/apt/sources.list
```

2) Install the GPG Directory Manager
```shell
sudo apt install dirmngr -y
```

3) Get the GPG signing key from Ububtu
```shell
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 93C4A3FD7BB9C367
```

4) Update the package manager from the new repo
```shell
sudo apt update
```

5) Add some common libraries
```shell
sudo apt install software-properties-common
```

6) Finally install Ansible and SSHpass to use passwords with Ansible
```shell
sudo apt install ansible sshpass
```

To validate that everything went ok and to confirm the version of Ansible installed use:

```shell
ansible --version

ansible [core 2.12.10]
  config file = /etc/ansible/ansible.cfg
  configured module search path = ['/home/xxxxxx/.ansible/plugins/modules', '/usr/share/ansible/plugins/modules']
  ansible python module location = /usr/lib/python3/dist-packages/ansible
  ansible collection location = /home/xxxxxx/.ansible/collections:/usr/share/ansible/collections
  executable location = /usr/bin/ansible
  python version = 3.9.2 (default, Feb 28 2021, 17:03:44) [GCC 10.2.1 20210110]
  jinja version = 2.11.3
  libyaml = True
```
### Docker

1) First we need to install Docker, this will take a while, be patient:

```shell
curl -sSL https://get.docker.com | sh
```

2) Add the current user to the permissions to run docker commands:

```shell
sudo usermod -aG docker ${USER}
```

3) Install some prerequisites to be able to use PIP
```shell
sudo apt-get install libffi-dev libssl-dev
sudo apt install python3-dev
sudo apt-get install -y python3 python3-pip
```
4) And now we can install docker-compose
```shell
sudo pip3 install docker-compose
```
5) Enable the Docker system service to start at boot time
```shell
sudo systemctl enable docker
```
NOTE: I then needed to reboot before Docker would work correctly (not sure why) but you can check docker is working correctly using:
```shell
docker run hello-world
```

### AWX Prerequisites

AWX has dependencies on NodeJS and a few other tools:
```shell
sudo apt install nodejs npm
sudo apt install python3-pip git pwgen unzip
sudo pip3 install requests==2.22.0 docker-compose==1.29.2
```










