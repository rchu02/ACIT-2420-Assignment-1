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

