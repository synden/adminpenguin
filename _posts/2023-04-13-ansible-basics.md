---
layout: post
title: Ansible Installation & Basics
subtitle: Simplify IT Operations with Ansible Automation
categories: linux
tags: [linux, ansible, ubuntu]
banner:
  image: ../assets/images/banners/ansible-ubuntu.jpg
  opacity: 0.618
  background: "#000"
  height: "70vh"
  min_height: "38vh"
  heading_style: "font-size: 3em; font-weight: bold"
  subheading_style: "color: #9580ff"
---
## Introduction
Ansible is an open-source automation tool that allows you to automate the configuration management, application deployment, and task automation. Ansible uses a simple and easy-to-learn syntax based on YAML that makes it easier to read and write automation tasks. In this tutorial, we will cover the basic concepts of Ansible and demonstrate how to install packages, update systems, and perform other tasks using Ansible.


## Installing Ansible
Before we begin, we need to install Ansible on our machine. Ansible can be installed on any Linux, macOS, or Windows machine. The easiest way to install Ansible on Linux is by using the package manager of your Linux distribution. For example, on Ubuntu, you can run the following command to install Ansible:
```bash
sudo apt-get update
sudo apt-get install ansible
```
Once Ansible is installed, you can check its version by running:
```bash
ansible --version
```


## Writing Ansible Playbooks
Ansible uses Playbooks to automate tasks. A Playbook is a YAML file that contains a set of tasks that Ansible will execute. Here is an example of a simple Playbook that installs the Nginx web server:
```yaml
---
- name: Install Nginx
  hosts: all
  become: yes
  tasks:
    - name: Install Nginx package
      apt:
        name: nginx
        state: present
```

**Let's break down this Playbook:**

* ```name```: A descriptive name for the Playbook.
* ```hosts```: The target hosts that Ansible will execute the tasks on. In this case, we're targeting all hosts.
* ```become```: This tells Ansible to elevate the privileges to become a superuser before executing the tasks.
* ```tasks```: A list of tasks that Ansible will execute.

The first task in this Playbook installs the **Nginx** package using the ```apt``` module. The ```name``` parameter specifies the name of the package to install, and the ```state``` parameter specifies that we want to make sure the package is installed.

### Running Ansible Playbooks
To run this Playbook, save it to a file named **install_nginx.yaml**, and run the following command:
```bash
ansible-playbook install_nginx.yaml
```

Ansible will connect to the target hosts and execute the tasks specified in the Playbook.

## Updating Systems
You can also use Ansible to update the system packages. Here's an example Playbook that updates the system packages:
```yaml
---
- name: Update packages
  hosts: all
  become: yes
  tasks:
    - name: Update packages
      apt:
        upgrade: dist
        update_cache: yes
```
This Playbook uses the ```apt``` module to update the system packages. The ```upgrade``` parameter specifies that we want to perform a distribution upgrade, and the ```update_cache``` parameter specifies that we want to update the package cache.

## Conclusion

In this tutorial, we covered the basic concepts of Ansible and demonstrated how to install packages, update systems, and perform other tasks using Ansible. Ansible is a powerful automation tool that can help you save time and increase productivity. With Ansible, you can automate almost any task, no matter how complex it is.
