# EAL_OpenBiblio_Setup
Setup tutorial for OpenBiblio at EAL (you can copy-paste commands)

* Install a Linux Virtual Machine (e.g. Ubuntu Server)
* Use Putty - you can copy-paste commands
* Once installed, download a LAMP server
    * During instalation: auto install MySQL and Apache2; or
    * for Ubuntu: __apt-get install lamp-server^__ 
* Download OpenBiblio
    * __wget http://downloads.sourceforge.net/project/obiblio/OpenBiblio/0.7.2/openbiblio-0.7.2.zip__
* Install unzip
    * __apt-get install unzip__
* Unzip openbiblio zip file
    * __unzip openbiblio-0.7.2.zip -d /var/www/__
* Start MySQL command line as root
    * __mysql -u root -p__
    * enter your MySQL password
* MySQL commands end with a semicolon ";"
* Create a new OpenBiblio database
    * __create database OpenBiblio /*!40100 default character set latin1 */;__
* Verify that it worked
    * __show database;__
    * You should see a small table with "OpenBiblio"
* Create a new MySQL user with priviliges to the OB database
    * user: _obiblio_user_,  password: _obiblio_password_
    * __grant all privileges on OpenBiblio.* to obiblio_user@localhost identified by 'obiblio_password';__
* Quit current MySQL session and login as obiblio_user
    * __mysql -u obiblio_user -p OpenBiblio__
* 
