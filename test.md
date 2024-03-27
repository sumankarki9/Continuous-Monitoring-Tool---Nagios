# Installation Nagios

To start Nagios Core installation, we must have a Linux server. Here are the steps for Nagios installation:

## Step 1:

Install prerequisite software like httpd, php, gcc Compiler, and gd development libraries on your machine to install Nagios.
Here are the commands:
```bash
sudo apt-get update -y
sudo apt install -y apache2 php gcc libc6 libc6-dev libgd-dev
```
## Step 2:
We need to create and set up a user account for the Nagios user:
```bash

sudo adduser -m nagios
passwd: nagios

# Create Group:
sudo groupadd nagiosgrp
sudo usermod -a -G nagiosgrp nagios
sudo usermod -a -G nagiosgrp apache
```
Step 3:
Download Nagios Core and the plugins. Now, we have to create a directory for storing the downloads.
```bash
mkdir -p ~/downloads
cd ~/downloads
```
# Now download the source code tarball of both Nagios and its plugins.
```bash
wget [URL]
wget [URL]
```
