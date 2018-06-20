# Linux-Server-438
### About
  This Project is about configuring the Linux-Server.

### Server Details

Server IP Address 52.66.124.9

Hosted site Url [http://52.66.124.9.xip.io/](http://52.66.124.9.xip.io/)

### How to connect as grader:

  save private key provided in your local machine and run the following command
  ```
  ssh -i path/to/privatekey -p 2200 grader@52.66.124.9
    
  ```
  
### Id_rsa key
```
-----BEGIN RSA PRIVATE KEY-----
MIIEpQIBAAKCAQEAv7OEuI2FvRDKIF3nxrVyFxVk3eMWjDvFezAMCm7n3etzF3Ub
kTTW2VzkprVGnRNiodWrCTBDeXhrILkMLlkdN9JL+O88BCGtwIKAiskAwxSCtHrQ
qnyM5nCNuZAD4Si2r2NdHSu5GzXf3ekwMU22xyr8+TReWl8AVIRUq6lhV3SsESl7
JCBqy2eCjW1DFFmTCYuYLKMngM1Gw+KUSrVPPuN9sPXDn82uMd6nEuTi88gCW6yh
AaPcVY+SS5Pw7Bz6xKamobYml6EAsxofg68rDM2J1OY/oottuPLy+aOfBu+thcNV
3RQBdcnXbfltCFgnXD8q82zryRXRpvEwhAwisQIDAQABAoIBAEOl/wT9dB93CE0J
tlvp9dvtgc3HcFKGWTcSin04C/zFNLUnb1X7loHYBRxLRiLyD1FazGOOs5DvDKbc
hk7oxaXIQWUUT1KJ6/3OT7wqGGm/GCzGVlKDZ1l+iJTeHHBdZLJZ1ycPIeBXT6vI
uWf8q653HhR3BYDQm5Y3qIV3XVF1zvYAUihsZebeKKKqvJxFcLJnW/TmobIF/kj7
EcZE+avPoKaY5ELWMJ0V+FEb9V5McjZiU9XNwVD4LJlremUjar6V9ZWRyhbvY+yQ
rT3n3aADufQ247PAYFQli8sPPq+I+g52dmmj/FCtQdnx6XF7yn9IzUOh40VHuh6E
hZ6zyAECgYEA7U4fjO2MEQVlj9S7OiRRMiLXRi0xwyJlWDOSl4oWIfrKN/yYuzNZ
nZjP8pEdsqMCSr71/gbnr1xFIXECoON/kL6yNzXKgcBHUGo2qXTs5ns36vM97IBJ
wS7n/r1/Mv6WCxGbp0WuzWSd847pQ7N9qlA3thwVosw/jZbsbkFNqDECgYEAzs2s
XB+MlmWrs5hYx6xBOER4zsSrYKoUSetGsRnasnn7F5wEF7D01ERe6Kz9WHjeEGan
7yVbQF7Ke/527OmF9abLk5cZBVMLa0d0NKSDr+i9hp5CGb5Pk36huAAGP/fWpRVX
MV/KLZs4uYSVztuK0qUooASL3YwKa4h06V26AoECgYEAvjfyOHAt53Lw/0MhtTBp
WYvuDdWqXuWSYQouBoTsyt4R/KDg+KXnvtlATwsdyBS8gJfj7XUxgDKxQ2YoGjli
Bu+lQXY/1pP/VildmaYdQ38fypiiWZJYDJ+B3YOek4zZTxQVNhc4UHHH3vT+bINT
RxM4JSUL/sxEYUXKTXLRQfECgYEAoOWaPU56hiTyMtfL8wYM9Ccpys1u/NU21dAM
fwu7gHKxLcw/zuLpiSDsqqC0t5nKQ/5qmAB7f5iAd3oisu55QAeWiezcFa1ny/6a
5b49iqZMlqkYiojrxriWP98c/bXotSXmYc7CMTt8JbKHD5r15i+DbQQ8gZFMJh/T
viEi8IECgYEApwwlGlh/o2F7em3ybhJh/qsn+KatXApUAOiU5jXxj6w89UwjHQ8u
O8GrZ1I/28keaYK3x2HLMWtI6X+EsBj9u2w0Brszy8njjvWRivaVpkJ+HqooCG6M
oTcZrX79MfakU7yDCTtYnP1BKMmgVsab1FlYyn6Fvh2YeteS23yCKYQ=
-----END RSA PRIVATE KEY-----
```
### grader password
```
surya
```
### Configuring Linux Server

#### Updating all packages
```
sudo apt-get update
sudo apt-get upgrade
```

#### Creating grader User:
  ```
  sudo adduser grader
  ```
  This will add new user
  ```
  sudo nano /etc/sudoers
  ```
  Below the Root user append the following line
  ```
  grader  ALL=(ALL:ALL) ALL
  ```
  This will grant sudo permission to grader
  #### Creating a ssh key pair for grader
   On your local machine in terminal/command prompt type
   ```
   ssh-keygen
   ```
   Which will generate the public and private ssh keys which is saved to .ssh folder
   
   Then in your virtual machine change to newly created user
   ```
   su - grader
   ```
   Create a new directory .ssh and new file authorized_keys in that directory
   ```
   mkdir .ssh
   sudo nano .ssh/authorized_keys
   ```
   Copy the public key with .pub extension to authorized_keys and save the file
   ```
   chmod 700 .ssh
   chmod 644 .ssh/authorized_keys
   ```
   - 700 will give read write and execute permission to user.
   - 644 prevent other user from writting in to file.
   Then restart ssh server
   ```
   service ssh restart
   ```
   
   Log in to grader with private key generated 
   ```
   ssh -i .ssh/id_rsa grader@ipaddress 
   ```
  #### Changing the ssh port to 2200
   ```
   sudo nano /etc/ssh/sshd_config
   ```
    
   Restart the ssh server
   
   ```
   service ssh restart
   ```
   
   >Note: Before Logging using ssh add custom TCP port 2200 under lightsaail firewall in networking tab in lightsail instance console  
   
   Now Login using command like this
   ```
   ssh -i .ssh/id_rsa -p 2200 grader@youripaddress
   ```
   
  #### Disabling ssh login as root
  `sudo nano /etc/ssh/sshd_config`
  
  make change `PermitRootLogin no`
  
  #### Configurating  Ufw firewall
  ```
  sudo ufw status
  sudo ufw allow 2200/tcp
  sudo ufw allow 80/tcp
  sudo ufw allow 123/udp
  sudo ufw enable
  ```
  This will allow all required ports and enables the ufw
  ```
  sudo ufw status
  ```
  It will display all allowed ports
  
  #### Changing time Zone
  `sudo dpkg-reconfigure tzdata`
  
  select none from list and then select utc.
  
  #### Installing Apache2 
  In terminal 
  
  ```sudo apt-get install apache2```
  
  Now mod_wsgi
  
  ```sudo apt-get install python-setuptools libapache2-mod-wsgi```
  
  Enable mod_wsgi
  
  ```sudo a2enmod wsgi ```
  ##### Setting up your flask application to work with apache2
   Creating a flask app
   
   In /var/www directory create a new folder
   `sudo mkdir FlaskApp`
   
   Install git 
   
   `sudo apt-get install git`
   
   move to the FlaskApp `cd FlaskApp`
   
   In that direcory clone your github repository
   
   `sudo git clone https://github.com/username/catalog.git`
   
   Rename your repository to FlaskApp
   
   Then rename your project file to `__init__.py`
   
   >Error : While accesssing the client_secrets.json file 
   ```
   PROJECT_ROOT = os.path.realpath(os.path.dirname(__file__))
   json_url = os.path.join(PROJECT_ROOT, 'client_secrets.json')
   CLIENT_ID = json.load(open(json_url))['web']['client_id']
   ```
   Use json_url instead client_secrets.json in script
   
  ##### Install and configuring postgresql for project
   Install Postgres `sudo apt-get install postgresql`
   
   login to postgres `sudo su - postgres`
   
   postgres shell `psql`
   
   create user `CREATE USER catalog WITH PASSWORD 'password';`
   
   permit user to createdb `ALTER USER catalog CREATEDB;`
   
   Create a db name  catalog with user catalog `CREATE DATABASE catalog WITH OWNER catalog;`
   
   connect to db `\c catalog`
   
   revoke all permission to public `REVOKE ALL ON SCHEMA public FROM public;`
   
   Give schema permission to user catalog `GRANT ALL ON SCHEMA public TO catalog;`
   
   exit from db and postgres `\q and exit`
   
   Change the database connection in both db_setup.py and `__init__.py` as `engine =       create_engine('postgresql://catalog:password@localhost/catalog')`
   
   Now you are ready with your applicatiom
  #### Configure and Enable a New Virtual Host
   `sudo nano /etc/apache2/sites-available/FlaskApp.conf`
   
   In this add the following code
   ```
   <VirtualHost *:80>
		ServerName mywebsite.com
		ServerAdmin admin@mywebsite.com
		WSGIScriptAlias / /var/www/FlaskApp/flaskapp.wsgi
		<Directory /var/www/FlaskApp/FlaskApp/>
			Order allow,deny
			Allow from all
		</Directory>
		Alias /static /var/www/FlaskApp/FlaskApp/static
		<Directory /var/www/FlaskApp/FlaskApp/static/>
			Order allow,deny
			Allow from all
		</Directory>
		ErrorLog ${APACHE_LOG_DIR}/error.log
		LogLevel warn
		CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
   ```
   Enable the virtual host 
   `sudo a2ensite FlaskApp`
   
   Disabling the default apache2 page
   `sudo a2dissite 000-default.conf`
   
  #### Create the .wsgi File
    ```
    cd /var/www/FlaskApp
    sudo nano flaskapp.wsgi 
    ```
   Add the following code
   
   ```
   #!/usr/bin/python
    import sys
    import logging
    logging.basicConfig(stream=sys.stderr)
    sys.path.insert(0,"/var/www/FlaskApp/")

    from FlaskApp import app as application
    application.secret_key = 'Add your secret key'
   ```
   save and exit
   
   Deploying flask app with apache2 is referred from [Digital ocean](https://www.digitalocean.com/community/tutorials/how-to-deploy-a-flask-application-on-an-ubuntu-vps)
   
   #### Installing require modules
   You can either install all modules on your machine or create a virtual environment for the project and install the modules
   ` pip install flask sqlalchemy psycopg2 requests oauth2client`
   
   #### Setting up your Google Oauth2
   Login to your [developer console](https://console.developers.google.com) and select your project and edit OAuth details as following
   
   Javascript origin
   `http://ip.xip.io`
   
   redirect URI
   
   `http://ip.xip.io/login`
   
   `http://ip.xip.io/gconnect`
   
   `http://ip.xip.io/callback`
   
   [xip.io](xip.io) is a free DNS which will be the same as using IP address
   
   #### Final Step
   Restart your apache2 server
   
   `sudo service apache2 restart`
   
