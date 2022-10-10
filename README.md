# ANSIBLE
## A personal project for Ansible
### INSTALLING LAMP USING ANSIBLE


#### STEPS TO SETUP ANSIBLE HOSTS NAMES USING "MASTER and SLAVE(s)"

Assuming master and slave(s) is **already** configured properly either through a cloud service provider e.g AWS, Digital Ocean **OR** locally on your Desktop(two or more VMs)...

**THEN:**

**NOTE:: ALL STEPS MUST BE DONE IN MASTER ONLY**

**Step 1: Download Ansible on MASTER**

$ sudo apt update -y && apt upgrade -y && apt install ansible -y

**Step 2: Verify installation**

$ ansible --version

**Step 3: Creating the test inventory file**

**NOTE:** On your Exercise-7...

$ vi inventory.txt

**\_Edit file as followed using the IP address of your **SLAVE**\_**

========================================================

ubuntu-focal ansible_host=192.168.56.5 ansible_connection=ssh ansible_user=vagrant

========================================================

Quit and Save with :wq.

**Step 4: Execute the file**

$ ansible ubuntu-focal -m ping -i inventory.txt


**Step 5: Edit your web hosts**

$ sudo vi etc/ansible/host

Define your Hosts using the IP address(es) of your **SLAVE(s)**

**The host name **(myservers)** will be used in ansible playbook**


Quit and Save with :wq.

## **NEXT**

Login in as root

## MUST BE DONE ON SLAVE

Prerequisites: php7.4

Step 1: Make a Directory for your Site

You’ll create a directory for your site that you’ll be hosting, within the /var/www folder. This location newly created location is also dubbed the document root location; you’ll need to set this path later in the configuration file. Sub the phpdomain.com for your domain name.

$ mkdir -p /var/www/phpdomain.com/public_html

Step 2: Set Folder Permissions

$ chmod -R 755 /var/www

Step 3: Set up an Index Page

To see a home page you’ll want to make sure the index.php file is created for your domain. Something as simple as "The e.g given on LMS" can be set within this file.

$ vim /var/www/phpdomain.com/public_html/index.php

Save and quit by hitting the Escape button and typing :wq

Step 4: Copy the Config File for your Site

Copy the default configuration file for your site, this will also ensure that you always have a default copy for future site creation.

$ cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/phpdomain.com.conf

Step 5: Edit the Config File for your Site

At the bare minimum, you’ll adjust and add the highlighted lines within the <VirtualHost *:80> and tags.

Note:: ServerAlias is the alternative name for your domain, in this case and in most, you’ll put www in front of the domain name so people can view the site by either www or non www (ServerName).

$ vim /etc/apache2/sites-available/phpdomain.com.conf

edith as followed;

=====================================

<VirtualHost *:80>

ServerAdmin admin@example.com

ServerName phpdomain.com

ServerAlias www.phpdomain.com

DocumentRoot /var/www/phpdomain.com/public_html

ErrorLog ${APACHE_LOG_DIR}/error.log

CustomLog ${APACHE_LOG_DIR}/access.log combined

</VirtualHost *:80>

===================================

Quit and Save with :wq.

Step 6: Enable Your Config File

Out of the box, your server is set to read the default 000-default.conf file. But, in our previous step we made a new config file for your domain. So, we will need to disable the default file.

$ a2dissite 000-default.conf

$ a2ensite phpdomain.com.conf

We restart the Apache service to register our changes.

$ systemctl restart apache2

Step 7: Verify Apache Configurations

After starting Apache you now can view that the configurations are working by either editing your /etc/host file on your computer or by editing your domain's DNS.

After either one of these aspects are set, you'll be able to visit your website in a browser to see the index.php pages set in Step 3.

### **Check out the yaml file in the folder for the playbook.**



