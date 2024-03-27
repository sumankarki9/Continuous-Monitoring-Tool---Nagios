# Installation Nagios

To start Nagos Core installation we must have the linux server. Here is the Step to installation of Nagios:-

Step 1 :
install Pre-requisite software like httpd, php, gcc Compiler and gd development libraries on your machine to install nagios.
Here the command:-
$ sudo apt-get update -y
$ sudo apt install apache2 php
$ sudo apt install gcc
$ sudo apt install libc6
$ sudo apt install libc6-dev
$ sudo apt install libgd-dev

Step 2:
We need to create and setup a user account for nagios user:
$ sudo adduser -m nagios
 passwd: nagios

Create Group:
$ group add nagiosgrp
$ usermod -a -G nagiosgrp nagios
$ usermod -a -G nagiosgrp apache

Step 3:
Download nagios Core and the plugins. Now, we have to create a directory for storing the downloads.
$ mkdir ~/downloads
$ cd ~/downloads
Now download the source code tarball of both nagios and its pligins.
$ wget 

$ wget

step 4:
Extract and Compile the nagios sourcecode tarball.
$ tar zxvf nagios
$ cd nagios


Now run the configuration script with the name of the group which we have created in about step.

$ ./configure --with-command-group=nagiosgrp

Comile the Nagios source code.
$ make all

Now Install Binaries, init script, sample config files and set permissions on the external command directory.

$ make install #(to compile init script)
$ make install-init
$ make install-config
$ make install-commandmode

Step 5:
Configure the Web interface:
make install-webconf

Step 4:
Create a 'nagiosadmin' accounttt for login into the nagios web inferface.

$ httpd -c /usr/local/nagios/etc/htpasswd.users nagiosadmin
Now it will ask to set a new passwd .

Now restart the httpd:
$ service httpd restart

Step 7:
Extract, Compile and install the nagios pugins and sourcode tarball:-
Extract:
$ cd ~/downloads
$ tar zxvf nagios-plugins-2
$ cd nagios-plugins

Compile and install the plugins:
$ ./configure --with-nagios-usr=nagios --with-nagios-group=nagios
$ make
$ make install

Step 8:
start Nagios and add Nagios to the list of system services and have it automatically start when the system boots.
$ chkconfig --add nagios
$ chkconfig nagios on 


Step 9:
We need to verify the configuration files to start Nagios:-
$ /var/local/nagios/bin/nagios cfg
$ /var/local/nagios/etc/nagios cfg

If there are no errors, we can start nagios:

$ service nagios start
$ service httpd restart

Now Its live . You can access it from browser using its public or localhost ip.
eg: http://40.10.22.5/nagios or http://localhost/nagios
username : nagiosadmin
password: nagios@123