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

sudo adduser nagios
passwd: nagios

# Create Group:
sudo groupadd nagiosgrp
sudo usermod -a -G nagiosgrp nagios
sudo usermod -a -G nagiosgrp apache
```
## Step 3:
Download Nagios Core and the plugins. Now, we have to create a directory for storing the downloads.
```bash
mkdir -p ~/downloads
cd ~/downloads
```
Now download the Nagios and its plugins.
```bash
wget http://prdownloads.sourceforge.net/sourceforge/nagios/nagios-4.0.8.tar.gz

wget http://nagios-plugins.org/download/nagios-plugins-2.0.3.tar.gz
```

Extract and Compile the Nagios file.
```bash
sudo tar zxvf nagios-4.0.8.tar.gz 
cd nagios-4.0.8

 Now run the configuration script with the name of the group which we have created in the previous step.
./configure --with-command-group=nagiosgrp

Compile the Nagios source code.
sudo apt install make
sudo apt install make-guide
sudo make all

Now Install Binaries, init script, sample config files, and set permissions on the external command directory.
sudo make install  
sudo make install-init
sudo make install-config
sudo make install-commandmode

```
## Step 5:
Configure the Web interface:
```bash
sudo mkdir -p /etc/httpd/conf.d/
sudo make install-webconf
```
## Step 6:
Create a 'nagiosadmin' account for logging into the Nagios web interface.
```bash
sudo htpasswd -c /usr/local/nagios/etc/htpasswd.users nagiosadmin
```
 Now it will ask to set a new password.

Now restart the httpd :
```bash
sudo service apache2 restart
```
## Step 7:
Extract, Compile, and install the Nagios plugins and source code tarball:
``` bash
cd ~/downloads
tar zxvf  nagios-plugins-2.0.3.tar.gz
cd nagios-plugins-2.0.3
```
Compile and install the plugins:
```bash
./configure --with-nagios-usr=nagios --with-nagios-group=nagios
sudo make install
```
## Step 8:

Start Nagios and add Nagios to the list of system services and have it automatically start when the system boots.
``` bash

sudo update-rc.d nagios defaults

sudo systemctl enable nagios

```
## Step 9:
We need to verify the configuration files to start Nagios:
``` bash
sudo /usr/local/nagios/bin/nagios -v /usr/local/nagios/etc/nagios.cfg
```
if u get any issue like this : Error in configuration file '/usr/local/nagios/etc/nagios.cfg' - Line 452 (Check result path '/usr/local/nagios/var/spool/checkresults' is not a valid directory) Error processing main config file!

you can simple run this command to fix it:-

```bash
sudo mkdir -p /usr/local/nagios/var/spool/checkresults
sudo chown -R nagios:nagios /usr/local/nagios/var/spool/checkresults
```

If there are no errors, we can start Nagios:

```bash
sudo service nagios start
sudo service apache2 restart
```

Now it's live. You can access it from a browser using its public or localhost IP.
eg: `http://40.10.22.5/nagios/` or `http://localhost/nagios`
Username: nagiosadmin
Password: nagios@123