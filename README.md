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
    $ sudo ufw enable
    
  5. Modify sshd_config.
  
    $ sudo nano /etc/ssh/sshd_config
    
    Change 22 to 2200
    
  6. Add grader user and give sudo access
    $ sudo adduser grader
    $ sudo usermod -aG sudo grader
    
 7. 
