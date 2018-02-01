# Linux-server-project
Udacity Linux server project 


IP Address: 52.15.210.193
SSH Port: 2200
Website URL http://52.15.210.193/catalog

Software Installed on Linux Server. 
  1. POSTGRESQL
  
    $ apt-get install postgresql postgresql
  2. Apache2
  
    $ sudo apt-get install apache2 
  3. mod_wsgi
  
    $ sudo apt-get install libapache2-mod-wsgi
  4. flask
  
    $ pip install flask
    
  5. psycopg2
  
    $ pip install psycopg2
    
  6. oauth2client
  
    $ pip install oauth2client
  
  7. Git
    
    $ sudo apt-get install git

Configuration changes made

  1. Update linux server
  
    $ sudo apt-get update
    
  2. Upgrade linix server
  
    $ sudo apt-get upgrade
    
  3. Remove uneeded files.
  
    $ sudo apt-get autoremove
    
  4. Update firewall settings.
  
    $ sudo ufw default deny incoming
    $ sudo ufw default allow outgoing
    $ sudo ufw allow ssh
    $ sudo ufw allow 2200/tcp
    $ sudo ufw allow www
    $ sudo ufw allow 123/udp
    $ sudo ufw deny 22
    $ sudo ufw enable
    
  5. Modify sshd_config.
  
    $ sudo nano /etc/ssh/sshd_config
    
    Change 22 to 2200
    
  6. Add grader user and give sudo access
  
    $ sudo adduser grader
    $ sudo usermod -aG sudo grader
    
  7. Configure timezone to UTC.
 
    $ sudo dpkg-reconfigure tzdata
    Scroll down till you get to UTC
    
  8. Configure PostgreSQL
  
    $ sudo -i -u postgres
    $ psql
    # CREATE USER catalog with PASSWORD 'catalog';
    # GRANT ALL PRIVILEGES ON catalog TO catalog;
    
  9. Create directory for project.
  
    $ cd /var/www
    $ sudo mkdir python
    $ cd python
    $ sudo mkdir catalogApp
    $ cd catalogApp
    $ sudo mkdir catalog
   
  10. Pull project from github.
    
    $ cd /var/www/python/catalogApp/catalog
    $ sudo git init
    $ sudo git pull https://github.com/heisenfraud/catalogServerApp
    
  11.  Setup flask virtual environment.
  
    $ cd /var/www/python/catalogApp/catalog
    $ sudo pip install virtualenv
    $ sudo apt-get install python-virtualenv
    $ virtualenv venv
    $ . venv/bin/activate
    $ pip install Flask
    $ deactivate
    
  12. Configure /etc/apache2/sites-enabled/000-default.conf file
  
    $ sudo nano /etc/apache2/sites-enabled/000-default.conf
    
    All the following text
    
    <VirtualHost *:80>

        ServerAdmin webmaster@localhost
        DocumentRoot /var/www/


        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined


        WSGIDaemonProcess catalog
        WSGIScriptAlias / /var/www/python/catalogApp/catalog.wsgi

        <Directory /var/www/python/catalogApp/catalog/>
            WSGIProcessGroup catalog
            WSGIApplicationGroup %{GLOBAL}
            Order deny,allow
            Allow from all
        </Directory>

    </VirtualHost>

    # vim: syntax=apache ts=4 sw=4 sts=4 sr noet
    
  13. Create WSGI file for application.
    
    $ cd /var/www/python/catalogApp
    $ sudo nano /var/www/python/catalogApp/catalog.wsgi
    
    Add the following to the file.
    
      import sys
      import logging
      logging.basicConfig(stream=sys.stderr)
      sys.path.insert(0,'/var/www/python/catalogApp')

      from catalog import app as application
      application.secret_key='super_secret_key'


Setting up application.
  
  1. Go into catalog directory and create database.
    
    $ cd /var/python/catalogApp/catalog
    $ sudo python categoryCreator.py

Third party resources.

  1. http://flask.pocoo.org/
  2. https://unix.stackexchange.com
  3. https://www.postgresql.org/
  4. https://stackoverflow.com
  5. https://httpd.apache.org/
  6. https://discussions.udacity.com
  
Author: Doug Mello
Version: 1.0
