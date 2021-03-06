# Project Code X Lab
#### Members: Joan Chirinos (PM), Anton Danylenko, Maryann Foley, and Susan Lin
---
#### Overview
This website provides a quick and easy way for those who are new to coding to work on projects and collaborate with their peers. Since everything is run in the browser, there is no need to install extra apps and detract from the main goal of writing the code itself.

The live code editor (via ajax) provides syntax highlighting and the overall functionality of the site provides a meaningful path towards productivity.

Our project implements Google OAuth as well. In addition, as a stretch goal, we hope to send emails to users regarding project notifications and invitations etc.

A database includes tables for files, projects, permissions, and users.

---
#### Demo
[Watch our video demo here](https://youtu.be/bI0_xEc8uHc)

---

## How to Run
### Install and run on localhost
1. Navigate to desired directory and clone the CodeXLab repo
2. Install python3 pip by running `$ apt-get install python3-pip`
3. Install virtualenv by running `$ pip3 install virtualenv`
4. Make a virtual environment by running `$ virtualenv <path/to/customVenvName>`
5. Open your virtual environment by running `$ flask <path/to/customVenvName>/bin/activate'
6. Install flask by runnning `$ pip3 install Flask`
7. Run the app by running `$ python3 __init__.py`

### Install and run on Apache2
#### NOTE: You may have to format most commands with `$ sudo <command>`
0. Set up an Ubuntu droplet
1. Run `$ sudo apt install apache2`, followed by `$ sudo ufw allow in "Apache Full"`
2. Run `$ sudo apt-get install libapache2-mod-wsgi-py3`
3. Clone repo into `/var/www/CodeXLab/`, creating directories if needed. Your directory structure should now be similar to the following
4. Run `$ sudo apt-get install python3-pip`
5. Run `$ sudo apt install python3-flask`
6. Write the following into `/etc/apache2/sites-available/CodeXLab.conf`, replacing the IP address

```
<VirtualHost *:80>
                ServerName <your.ip.address.here>
                WSGIScriptAlias / /var/www/CodeXLab/codexlab.wsgi
                <Directory /var/www/CodeXLab/CodeXLab/>
                        Order allow,deny
                        Allow from all
                </Directory>
                Alias /static /var/www/CodeXLab/CodeXLab/static
                <Directory /var/www/CodeXLab/CodeXLab/static/>
                        Order allow,deny
                        Allow from all
                </Directory>
                ErrorLog ${APACHE_LOG_DIR}/error.log
                LogLevel warn
                CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```

7. Run `$ sudo a2ensite CodeXLab`
8. Write the following into `/var/www/CodeXLab/codexlab.wsgi`

```
#!/usr/bin/python3
import sys
import logging
logging.basicConfig(stream=sys.stderr)
sys.path.insert(0, '/var/www/BigToe/')
sys.path.insert(1, '/var/www/BigToe/BigToe')

from BigToe import app as application
application.secret_key = 'Add your secret key'
```

9. Navigate to `/var/www/BigToe/BigToe/`
10. Run `$ chmod -R 755 data/`
11. Run `$ python3 util/db.py`. Your directory structure should now be similar to
12. Run `$ chmod -R 755 data/`
13. Run `$ sudo systemctl reload apache2`


## OAuth
- To be implemented

## Dependencies
### Python 3
We are using Python 3 as our primary language to facilitate scripting and to utilize the dependencies below.
We use the following __modules__:
1. __sqlite3__ (to utilize our sqlite3 database `tuesday.db`)
2. __uuid__ (to create unique identifiers for projects and messages)
3. __json__ & __request__
