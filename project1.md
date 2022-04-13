# Project-1

**process_through_project-1**

`sudo apt update`

`sudo apt install apache2`

`sudo systemctl status apache2`

![apache-status](./images/apache-status.png)

*first web server has just been launched in the clouds* 
*hurray!!!!!*

*the next step is to try and access it in*
*our ubuntu shell*
*first we ran this command on our terminal*

`curl http://localhost:80`
> now its time to check how our Apache HTTP server can respond to requests from the internet

*now we access the following url on our web browser*

[Apache_HTTP_server](https://18.207.206.64:80)

![ubuntu-status](./images/ubuntu-status.png)

*hurray!!!*

## Installing MYSQL

*we have to run the following command*

`sudo apt install mysql-server`

`sudo mysql_secure_installation`

*after achieving the result without any error, its time to test it*
*by runing this command*

`sudo mysql`
*after running the commabnd sucessfully we got an output like ds*
> Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 11
Server version: 8.0.22-0ubuntu0.20.04.3 (Ubuntu)

Copyright (c) 2000, 2020, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> 

*you can exit mysql console by typing this command*
`mysql> exit`

### Installing PHP
*run the following command*
`sudo apt install php libapache2-mod-php php-mysql`
`php -v`
> PHP 7.4.3 (cli) (built: Oct  6 2020 15:47:56) ( NTS )
Copyright (c) The PHP Group
Zend Engine v3.4.0, Copyright (c) Zend Technologies

*LAMP stack is fully installed and operational*
- Linus (Ubuntu)
- Apache HTTP Server
- MySQL
- PHP

# Creating a virtual host for your website using apache
*create directory for projectlamp using 'mkdir'*
`sudo mkdir /var/www/projectlamp`

*next is to assign ownership to the directory*
` sudo chown -R $USER:$USER /var/www/projectlamp`
> <VirtualHost *:80>
    ServerName projectlamp
    ServerAlias www.projectlamp 
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/projectlamp
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>

*I Save and closed  the file using the following directory*
- hit the esc button
- type :
- type wq.
- then hit entet to save file.

*i used the ls command to show the new file*
`sudo ls /etc/apache2/sites-available`
*you can now use a2ensite command to enable the new virtual host*
`sudo a2ensite projectlamp`
`sudo a2dissite 000-default`
*to make sure your configuration file doesnt contain syntax errors, run this command*
`sudo apache2ctl configtest`

*so i finally reloaded apache so the changes can take effect*
`sudo systemctl reload apache2`

![sudo-systemctl](./images/sudo-systemctl-reloaded.png)

*I then created an index.html file in that location to test if the virtual host works as expected*

`sudo echo 'Hello LAMP from hostname' $(curl -s http://169.254.169.254/latest/meta-data/public-hostname) 'with public IP' $(curl -s http://169.254.169.254/latest/meta-data/public-ipv4) > /var/www/projectlamp/index.html`

*i opened the website url using ip-address in my browser*
`http://<Public-IP-Address>:80`
`http://<Public-DNS-Name>:80`

**ENABLE PHP ON THE WEBSITE**
`sudo vim /etc/apache2/mods-enabled/dir.conf`
`<IfModule mod_dir.c>
        #Change this:
        #DirectoryIndex index.html index.cgi index.pl index.php index.xhtml index.htm
        #To this:
        DirectoryIndex index.php index.html index.cgi index.pl index.xhtml index.htm
</IfModule>`

`sudo systemctl reload apache2`
*i created a new file named index.php inside the custom web root folder*
`vim /var/www/projectlamp/index.php`

![PHP-STATUS](./images/PHP-status.png)g