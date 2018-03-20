# Linux Server
This repository contains the project for Udacity Linux Server Configuration

## Requirements
Terminal Client to Run SSH into Linux.

## Connection Details
URL: http://eo-u1604-vm3.southcentralus.cloudapp.azure.com  
IP Address: 13.84.186.157

Connection: `ssh grader@13.84.186.157 -p 2200 -i /location_of_rsa_key`
User: grader

## Project Overview
This repository covers the requirements for Udacity - Full Stack Web Development Item Catalog project.

This project was created using a Virtual Machine running Ubuntu 16.04.3 LTS.  
The machine is located in Microsofts Azure Cloud Computing Platform and Services.

On deployment the machine was upgrade through:
- `sudo apt-get update`
- `sudo apt-get upgrade`

The following configurations were performed on the server:  
Timezone was upgraded thorugh `sudo dpkg-reconfigure tzdata`. Select None of the Above. Select UTC.

### 1. Packages
The following packages were installed through `sudo apt-get install`
- Apache: `apache2`
- WSGI: `libapache2-mod-wsgi-py3`
- PostgreSQL: `postgresql`
- Git: `git`
- Pip3: `python3-pip`

### 2. Security
1. Enable ports 2200, 80, and 123 in Azure.
2. Change SSH port to 2200, disable password based authentication, and disable remote login by root by running:
   - `sudo nano /etc/ssh/sshd_config`
   - Change the port to `Port 2200`
   - Change `PasswordAutherntication` to `no`
   - Change `Permit`
3. Configure Uncomplicated Firewall:
   - `sudo ufw default deny incoming`
   - `sudo ufw default allow outgoing`
   - `sudo ufw allow 2200/tcp`
   - `sudo ufw allow www` or `sudo ufw allow 80/tcp`
   - `sudo ufw allow 123/tcp`
   - `sudo ufw enable`

### 3. Grader User Details
1. Create user 'grader' through `sudo adduser grader`
2. Give sudo permissions to grader through:
    - Copy sudoers file: `sudo cp /etc/sudoers.d/eoadmin /etc/sudoers.d/grader`
    - Replace username in file to `grader`
3. Create an SSH pair for grader by running:
    - Create RSA key: `ssh-keygen`. Key will be located in resulting .pub file.
    - Run `sudo nano .ssh/authorized_keys` and copy Public Key in this file. Save Changes.
4. Secure the directories with the RSA Keys:
    - `sudo chmod 700 .ssh` (Only user can read, write, execute)
    - `sudo chmod 644 .ssh/authorized_keys` (Use can read and write, others can only read)

### 4. PostgreSQL Setup
1. Create *catalog* database through `CREATE DATABASE catalog`
2. Setup & initialize the database:
   - Setup:`python /var/www/html/Item_Catalog/Item_Catalog/database_setup.py`
   - Initialize:`python /var/www/html/Item_Catalog/Item_Catalog/initialize_database.py`
2. Login to the database `psql -d catalog`
3. Add new users *www-data* and *www* to ensure psycop2g compatibility `createuser username`
4. Grant permissions to new user for CRUD operations
   - `GRANT SELECT, INSERT, DELETE,UPDATE ON category to "www-data";`
   - `GRANT SELECT, INSERT, DELETE,UPDATE ON category to "www";`
5. Exit the database with `\q`

### 5. WSGI Setup
1. Modify the default site through `sudo nano /etc/apache2/sites-enabled/000-default.conf`
2. Enter the following code after the first set of commentary:  
   ```ServerName eo-u1604-vm3.southcentralus.cloudapp.azure.com
    WSGIScriptAlias / /var/www/html/Item_Catalog/app_WSGI.wsgi
    <Directory /var/www/html/Item_Catalog/Item_Catalog/>
      Allow from all
      Order deny,allow
    </Directory>

    Alias /static /var/www/html/Item_Catalog/Item_Catalog/static/

   <Directory /var/www/html/Item_Catalog/Item_Catalog/static/>
          Allow from all
          Order deny,allow
   </Directory>```
3. Restart apache `sudo apache2ctl restart`

### 6. Item Catalog Application
1. Navigate to the app's desired directory through `cd /var/www/html`
2. Initialize git on the folder `sudo git init`
3. Clone GitHub repository for Item_Catalog `sudo git clone https://github.com/cseHdz/Item_Catalog.git`
4. The app is located in the local_flask branch `sudo git reset --hard origin/local_flask`
5. The following packages were installed through `sudo -H pip3 install`
   - Flask `Flask`
   - SQLAlchemy `sqlalchemy`
   - Psycopg2 `psycopg2`
   - oauth2client `oauth2client`
