# Linux Server
This repository contains the project for Udacity Linux Server Configuration

## Requirements
Terminal Client to Run SSH into Linux.

## Connection Details
IP Address: 13.84.186.157

To SSH into the machine, use the following user and RSA key pairs:  
- User: grader
- RSA Key: ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDIiaUNkstgtwAW58+5RCIFpDA1F4l4Kx1Lw18bzIPprn0ysC6vHlzhnmu1FKS1d3KSM37cqG8+8b8Wi4+bCsxUddbByS4EoRYbFwciN1hJerOLatv1uZAI3Hf/mfor2uHFRFEl18TinvbSRViaUMEt1I+w6ibEHFF2dZFRW4sLykc4oEvV1U+I3zXn3CfL1SmDvw2RIK9xUKZ8OlzNU/vuPyFVX3EMN6rhY7rqHQLq32MdZK5I3StishZNWICxAFZj2obbJSQk3V+sSGhdOs/So+eo6fKB0dVeRws6aNYCNJpGz749DCJmTb5y5F7Z1BNjlPMXAJklSERMFi0f/pjN carloshernandez@Carloss-MacBook-Pro.local
*Also found on the repository files as udacity_grader.pub*

Connection: `ssh grader@13.84.186.157 -p 2200 -i /location_of_rsa_key`

## Project Overview
This repository covers the requirements for Udacity - Full Stack Web Development Item Catalog project.

This project was created using a Virtual Machine running Ubuntu 16.04.3 LTS.  
The machine is located in Microsofts Azure Cloud Computing Platform and Services.

On deployment the machine was upgrade through:
- `sudo apt-get update`
- `sudo apt-get upgrade`

The following configurations were performed on the server:

### 1. Packages
The following packages were installed through `sudo apt-get install`
- Apache: `apache2`
- WSGI: `libapache2-mod-wsgi`
- PostgreSQL: `postgresql`

### 2. Security
1. Enable ports 2200, 80, and 123 in Azure.
2. Change SSH port to 2200 and disable password based authentication by running:
   - 
3. 

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
