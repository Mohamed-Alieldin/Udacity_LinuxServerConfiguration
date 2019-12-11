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
Server IP: **3.123.57.98** (Not Valid Anymore)
SSH Port: **2200**

## Application Url
http://3.123.57.98.xip.io
or
http://3.123.57.98
These are the urls that was used in the project delivery. They are not valid anymore.

## Software Summary
The software running on the server is a web application called "Item Catalog". This was the second project requested in my Udacity Full Stack Web Development Nano Degree Program.
You can find the project [here](https://github.com/Mohamed-Alieldin/Item-Catalog).
As a summary, the applicaiton preview different sports categories each with a group of sports items with their description. Google Authentication is used to enable log in for users. Each user can add items and edit or delete his items.

## Server Configurations
#### Updating Packages
1. Use the command `sudo apt-get update`  to detect the updates for the current packages.
2. Use the command `sudo apt-get dist-upgrade` to apply the updates.
#### Firwall configurations
1. Close all incoming requestes `sudo ufw default deny incoming`
2. Enable all outgoing requests `sudo ufw default allow outgoing`
3. Allow only the ports needed:
    * `sudo ufw allow ssh`
    * `sudo ufw allow www`
    * `sudo ufw allow ntp`
4. Activate the firewall `sudo ufw enable`

#### User Management
1. Prevent root user login by changing the value of "**PermitRootLogin**" to "**no**" in "sshd_config" file.
Steps:
    - `sudo nano /etc/ssh/sshd_config`
    - search for "**#PermitRootLogin prohibit-password**" and change it to be "**PermitRootLogin no**"
2. Adding user "**grader**" `sudo adduser grader`
2. Adding user **grader** to the sudo list `sudo adduser grader sudo`

#### Time Zone Configuration
Run `sudo dpkg-reconfigure tzdata` and then choose UTC as required in this project.

#### Required Installations
1. Install python3 `sudo apt-get install libapache2-mod-wsgi-py3`
2. Install Git `sudo apt install git`
3. Install pip3 `sudo apt install python3-pip`
4. Install SQLAlchemy `sudo pip install flask-sqlalchemy`
5. Install PostgreSQL `apt-get install postgresql postgresql-contrib`
By default, remote connections are disabled to postgreSQL
6. Create Catalog database `sudo -u postgres createdb catalog`

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
5. Run the app as WSGI app
To run the application as a wsgi app on apache, follow this [guide](http://terokarvinen.com/2016/deploy-flask-python3-on-apache2-ubuntu) 
6. Now you can browse the application http://3.123.57.98.xip.io.

#### Third Parties Source Lists
1. I used [amazon lightsail](https://lightsail.aws.amazon.com) to get the server for hosting my application.
2. I used [xip.io](http://xip.io/) instead of creating a domain name.
 
## SSH Keys Generation
I created an SSH key locally using the service keygen".
The private key location is "**/home/vagrant/.ssh/linuxCourse**".
Then I created the specified file on my server to store the public key to enable ssh key authentication.
* First, Create "**authorized_keys**" file in "**.ssh**" folder. `sudo touch .ssh/authorized_keys`.
* Second, Edit the file. `sudo nano .ssh/authorized_keys`
* Third, Add the public key to the file, save, and exit.


