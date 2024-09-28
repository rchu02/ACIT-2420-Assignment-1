# How to Set Up a Arch Linux Droplet Using Doctl

### Table of Contents

1. Introduction
2. Task 1: Creating SSH key
3. Task 2: Installing Doctl
4. Task 3: Cloud-init

### Introduction

This tutorial will guide you through the steps that allows you to make your own Arch Linux Droplet using doctl. 

What is Arch Linux?
Arch Linux is an open source Linux distribution which is a minimal base system, that can be configured by the users for what they want (1).

What is a Droplet?
Droplets from DigitalOcean are Linux-based Virtual Machines(VMs) that run on virtualized hardware (2).

What is Doctl?
Doctl is the DigitalOcean command line interface (CLI) (3).

By the end of this tutorial, you will be able to learn how to:
- Create your own SSH keys on your local machine.
- Install doctl on your Arch Linux machine.
- Connect your Digital Ocean account to your Arch Linux machine using doctl. 
- Use cloud-init to download all necessary packages through doctl.
- Create a new droplet using doctl.

### Task 1: Creating SSH key

**Overview:** This task will help you create your own SSH key pair (a private and public key) which will be used to connect to your digital ocean droplet.

1. **Make a SSH key**
Use the following command,
```
ssh-keygen -t ed25519 -f ~/.ssh/doctl-key -C "USERNAME"
```

In this case the USERNAME can be your username or your email. 
-  ssh-keygen: OpenSSH authentication key utility that is built in into your OS machine.
-  -t: Specifies the type of key to create. In this case it would be the default "ed25519". 
-  -f: *filename* Specifies the filename of the key file.
-  ~: The home directory.
- -C: Provides a new comment.

It will prompt you for a password, however just press *Enter* twice to have no password for your SSH key.

2. **Check if SSH key is in our system**
Now we should check if we have our SSH key in our ssh directory, type this command in your terminal
```
ls ~/.ssh
```
to check if files "doctl-key", which is your private key (do not share this) and "doctl-key.pub", which is your public key to use to make the droplet, are listed.

- cd: This is used to change directory.
- .ssh: The SSH key directory.
- ls: This is used to list all the files and directories in the current directory that you are in.

Congratulations, you have now created your own SSH keys.
