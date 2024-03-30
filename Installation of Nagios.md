# Installation Nagios

To start Nagios Core installation, we must have a Linux server. Here are the steps for Nagios installation:

## Step 1:

Install prerequisite software on your machine to install Nagios.
Here are the commands:
```bash
sudo apt-get update -y
sudo apt install wget unzip curl openssl build-essential libgd-dev libssl-dev libapache2-mod-php php-gd php apache2 -y
```
## Step 2:
Download Nagios Core and the plugins. Before that, we have to create a directory for storing the downloads.
```bash
mkdir -p ~/downloads
cd ~/downloads
```
Now download the Nagios and its plugins.
```bash
wget https://assets.nagios.com/downloads/nagioscore/releases/nagios-4.4.6.tar.gz

 wget https://nagios-plugins.org/download/nagios-plugins-2.3.3.tar.gz
```

Extract and Compile the Nagios file.
```bash
sudo tar -zxvf nagios-plugins-2.3.3.tar.gz
cd nagios-plugins-2.3.3 
```
run the Nagios Core configuration script
```bash
sudo ./configure 
```
Compile the Nagios source code
```bash
sudo make all
```
## Step 3:
Now we have to Make and install group and user and add directories to group
```bash
sudo make install-groups-users
```
Now we have to Add www-data directories user to the nagios group.
```bash
sudo usermod -a -G nagios www-data
```
## Step 4:
Now we can insall Nagios, configuration files and scripts,web interface, enabling rewrite mode and CGI config:

```bash
sudo make install
```
Initialize all the installation configuration scripts.
```bash
sudo make install-init
```
Install sample config files.
```bash
sudo make install-config
```
Install apache files for web interface.
```bash
sudo make install-webconf
```
Enable apache rewrite mode.
```bash
sudo a2enmod rewrite
```
Enable CGI config.
```bash
sudo a2enmod cgi
```
Restart the Apache service.
```bash
sudo systemctl restart apache2
```
## Step 5:
Create a 'nagiosadmin' account for logging into the Nagios web interface and set the password when prompted
```bash
sudo htpasswd -c /usr/local/nagios/etc/htpasswd.users nagiosadmin
```
Now restart the httpd :
```bash
sudo service apache2 restart
```
## Step 6:
Extract, Compile, and install the Nagios plugins and source code tarball:
``` bash
cd ~/downloads
tar zxvf  nagios-plugins-2.0.3.tar.gz
cd nagios-plugins-2.0.3
```
Compile and install the plugins:
```bash
sudo ./configure --with-nagios-usr=nagios --with-nagios-group=nagios
sudo make install
```
## Step 7:
Enable Nagios service to run at system startup.
```bash
sudo systemctl enable nagios
```
## Step 8:
We need to verify the configuration files to start Nagios:
``` bash
sudo /usr/local/nagios/bin/nagios -v /usr/local/nagios/etc/nagios.cfg
```
If there are no errors, we can start Nagios:

```bash
sudo service nagios start
sudo service apache2 restart
```

Now it's live. You can access it from a browser using its public or localhost IP.
eg: `http://40.10.22.5/nagios/` or `http://localhost/nagios`
Username: nagiosadmin
Password: < enter the password that you created will creating nagios admin >