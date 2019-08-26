# Full Stack Web Developer Nanodegree program
## Linux Server Configuration

<a href="https://www.udacity.com/">
  <img src="https://s3-us-west-1.amazonaws.com/udacity-content/rebrand/svg/logo.min.svg" width="300" alt="Udacity logo">
</a>

## Table of Contents

- [Table of Contents](#table-of-contents)
- [Intro](#intro)
- [IP&SSH](#IP&SSH)
- [Software Summary](#Software-Summary)
- [Server Configurations](#Server-Configurations)
- [SSH Keys Generation](#SSH-Keys-Generation)

## Intro

This project focuses mainly on how to run and secure an ubuntu server to host a web application.

## IP&SSH
Server IP: **3.123.57.98**
SSH Port: **22**

## Application Url

http://3.123.57.98.xip.io:8000/

## Software Summary
The software running on the server is a web application called "Item Catalog". This was the second project requested in my Udacity Full Stack Web Development Nano Degree Program.
You can find the project [here](https://github.com/Mohamed-Alieldin/Item-Catalog).
As a summary, the applicaiton preview different sports categories each with a group of sports items with their description. Google Authentication is used to enable log in for users. Each user can add items and edit or delete his items.

## Server Configurations
#### Updating Packages
1. Use the command `sudo apt-get update`  to detect the updates for the current packages.
2. Use the command `sudo apt-get upgrade` to apply the updates.
#### Firwall configurations
1. Close all incoming requestes `sudo ufw default deny incoming`
2. Enable all outgoing requests `sudo ufw default allow outgoing`
3. Allow only the ports needed:
    * `sudo ufw allow ssh`
    * `sudo ufw allow www`
    * `sudo ufw allow ntp`
    * `sudo ufw allow 8000` where 8000 is the port that the application listens on.
4. Activate the firewall `sudo ufw enable`

#### User Management
1. Adding user "**grader**" `sudo adduser grader`
2. Adding user **grader** to the sudo list `sudo adduser grader sudo`

#### Time Zone Configuration
Run `sudo dpkg-reconfigure tzdata` and then choose UTC as required in this project.

#### Required Installations
1. Install python3 `sudo apt-get install libapache2-mod-wsgi-py3`
2. Install Git `sudo apt install git`
3. Install pip3 `sudo apt install python3-pip`
3. Install PostgreSQL `apt-get install postgresql postgresql-contrib`
By default, remote connections are disabled to postgreSQL
4. Create Catalog database `sudo -u postgres createdb catalog`

#### Running The Application
1. Clone the Item Catalog Project `git clone https://github.com/Mohamed-Alieldin/Item-Catalog.git`
2. Install the requirements packages `pip3 install -r requirements.txt`
3. cd into Item Catalog folder and run the following at order:
    * `sudo python3 models.py`
    * `database_Datafill.py`
4. To prevent remote access to .git folder, follow these steps:
  * Create **.htaccess** at the root of the server using this command `sudo touch .htaccess`.
  * Edit this file using the command `sudo nano .htaccess` and add the text "RedirectMatch 404 /\\.git".
  * Save and Exit.
5. To run the application in the background, cd in the folder Item Catalog and run the application using the command `nohup python3 application.py &`
6. Now you can browse the application http://3.123.57.98.xip.io:8000/.

#### Third Parties Source Lists
1. I used [amazon lightsail](https://lightsail.aws.amazon.com) to get the server for hosting my application.
2. I used [xip.io](http://xip.io/) instead of creating a domain name.
 
## SSH Keys Generation
I created an SSH key locally using the service keygen".
The private key location is "**/home/vagrant/.ssh/linuxCourse**".
Then I created the specified file on my server to store the public key to enable ssh key authentication.
* All the following commands should be created by the grader user, so either login with the grader user or run commands in behalf of grader user and this can be done as follows.
* First, Create "**authorized_keys**" file in "**.ssh**" folder. `sudo -u grader touch .ssh/authorized_keys`.
* Second, Edit the file. `sudo -u grader sudo nano .ssh/authorized_keys`
* Third, Add the public key to the file, save, and exit.

