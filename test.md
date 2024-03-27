# Installation Nagios

# To start Nagios Core installation, we must have a Linux server. Here are the steps to install Nagios:

# Step 1:
# Install prerequisite software like httpd, php, gcc Compiler, and gd development libraries on your machine to install Nagios.
# Here are the commands:
$ sudo apt-get update -y
$ sudo apt install apache2 php gcc libc6 libc6-dev libgd-dev

# Step 2:
# We need to create and set up a user account for the Nagios user:
$ sudo adduser -m nagios
Password: nagios

# Create Group:
$ sudo groupadd nagiosgrp
$ sudo usermod -a -G nagiosgrp nagios
$ sudo usermod -a -G nagiosgrp apache

# Step 3:
# Download Nagios Core and the plugins. Now, we have to create a directory for storing the downloads.
$ mkdir ~/downloads
$ cd ~/downloads
# Now download the source code tarball of both Nagios and its plugins.
$ wget [URL]
$ wget [URL]

# Step 4:
# Extract and Compile the Nagios source code tarball.
$ tar zxvf nagios
$ cd nagios

# Now run the configuration script with the name of the group which we have created in the previous step.
$ ./configure --with-command-group=nagiosgrp

# Compile the Nagios source code.
$ make all

# Now Install Binaries, init script, sample config files, and set permissions on the external command directory.
$ sudo make install # (to compile init script)
$ sudo make install-init
$ sudo make install-config
$ sudo make install-commandmode

# Step 5:
# Configure the Web interface:
$ sudo make install-webconf

# Step 6:
# Create a 'nagiosadmin' account for logging into the Nagios web interface.
$ sudo htpasswd -c /usr/local/nagios/etc/htpasswd.users nagiosadmin
# Now it will ask to set a new password.

# Now restart the httpd:
$ sudo service apache2 restart

# Step 7:
# Extract, Compile, and install the Nagios plugins and source code tarball:
# Extract:
$ cd ~/downloads
$ tar zxvf nagios-plugins-2
$ cd nagios-plugins

# Compile and install the plugins:
$ ./configure --with-nagios-usr=nagios --with-nagios-group=nagios
$ make
$ sudo make install

# Step 8:
# Start Nagios and add Nagios to the list of system services and have it automatically start when the system boots.
$ sudo chkconfig --add nagios
$ sudo chkconfig nagios on

# Step 9:
# We need to verify the configuration files to start Nagios:
$ sudo /usr/local/nagios/bin/nagios -v /usr/local/nagios/etc/nagios.cfg

# If there are no errors, we can start Nagios:
$ sudo service nagios start
$ sudo service apache2 restart

# Now it's live. You can access it from a browser using its public or localhost IP.
# eg: http://40.10.22.5/nagios or http://localhost/nagios
# Username: nagiosadmin
# Password: nagios@123
