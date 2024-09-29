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

### Task 2: Installing Doctl and Connecting DigitalOcean using an API.

**Overview**: This task will help guide you to install doctl on your terminal and creating your first droplet using doctl.

1. **Install Doctl**
First run 
```
sudo pacman -S doctl
```
- sudo: Raises your privileges to run certain commands
- pacman: Package manager from arch

2. **Create an API token**
Now we will create an API token and make it so it grants account access to doctl. Go to your DigitalOcean account, then on the left hand dashboard, click on **API**
<img src="assests/dashboard.png" alt="dashboard" width="150"/>

Click **Generate New Token**
<img src="assests/generate_new_token.png.png" alt="generate_new_token" width="450"/>

Enter your token name
<img src="assests/token_name.png" alt="token_name" width="450"/>

Select **Full Access**, this will grant you the token all scopes available
<img src="assests/full_access.png" alt="full_access" width="450"/>

Click **Generate Token**

3. **Now use the API token to grant access to Doctl**
Copy your personal access token from the DigitalOcean site, then go to your arch terminal and running the command
```
doctl auth init --context <NAME>
```
"NAME" is name you give you give to save the token.
- doctl auth init: Initializes doctl to use a specific account (3).
- --context: Specify a custom authentication context name (3).

Now there will be a prompt 
<img src="assests/enter_access_token.png" alt="enter_access_token" width="250"/>
Paste your personal access token from the DigitalOcean site. You should get a confirmation: 
<img src="assests/validating_token.png" alt="dashboard" width="450"/>

Now we will switch to your account by running 
```
doctl auth switch --context <NAME>
```
Where "Name" is the input that you used when you initialized your authorization. 
- switch: Allows you to switch between authentication contexts you have already created (3).

Finally check if your account is connected by running
```
doctl account get
```
Where you can get the following details of your account profile (3):
- Email address
- Team
- Account Droplet limit
- Email verification status
- UUID for the account
- Account status (active or disabled).

Confirm the details and now you have connected your account to your arch.

4. Connect your SSH key to DigitalOcean

First use the command,
```
cat ~/.ssh/doctl-key.pub
```
your public SSH key should show up. Now copy the key.
- cat: Show contents of a file all at once (3).

Then type the command (**Note: Do not copy this code as your clipboard will forget your SSH key that copied in the previous step**)
```
doctl compute ssh-key "<KEYNAME>" create --public-key "<Paste your key in here>"
```
where you name your key and paste your public SSH key in the following brackets.
- doctl compute ssh-key create: Adds a new SSH key to your account (3).
- --public-key: Key contents (3).