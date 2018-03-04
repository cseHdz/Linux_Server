# Linux Server
This repository contains the project for Udacity Linux Server Configuration

## Requirements
Terminal Client to Run SSH into Linux.

## Connection Details
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
- WSGI: `libapache2-mod-wsgi`
- PostgreSQL: `postgresql`
- Git: `git`

### 2. Security
1. Enable ports 2200, 80, and 123 in Azure.
2. Change SSH port to 2200, disable password based authentication, and disable remote login by root by running:
   - `sudo nano /etc/ssh/sshd_config`
   - Change the port to `Port 2200`
   - Change `PasswordAutherntication` to `no`
   - Change `Permit
3. Configure Uncomplicated Firewall:
   - `sudo ufw default deny incoming`
   - `sudo ufw default allow outgoing`
   - `sudo ufw allow 2200/tcp`
   - `sudo ufw allow www` or `sudo ufw allow 80/tcp`
   - `sudo ufw allow 123/tcp`
   - `sudo ufw enable`

### 3. User Details
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
    
### 4. Item Catalog Application
