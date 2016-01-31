# EAL_OpenBiblio_Setup
Setup tutorial for OpenBiblio at EAL (you can copy-paste commands)

* Install a Linux Virtual Machine (e.g. Ubuntu Server)
* Use Putty - you can copy-paste commands
* Once installed, download a LAMP server
    * During instalation: auto install MySQL and Apache2; or
    * for Ubuntu: __`apt-get install lamp-server^`__
* Download OpenBiblio
    * __`wget http://downloads.sourceforge.net/project/obiblio/OpenBiblio/0.7.2/openbiblio-0.7.2.zip`__
* Install unzip
    * __`apt-get install unzip`__
* Unzip openbiblio zip file
    * __`unzip openbiblio-0.7.2.zip -d /var/www/`__
* Start MySQL command line as root
    * __`mysql -u root -p`__
    * enter your MySQL password
* MySQL commands end with a semicolon ";"
* Create a new OpenBiblio database
    * __`create database OpenBiblio /*!40100 default character set latin1 */;`__
* Verify that it worked
    * __`show database;`__
    * You should see a small table with "OpenBiblio"
* Create a new MySQL user with priviliges to the OB database
    * user: _obiblio_user_,  password: _obiblio_password_
    * __`grant all privileges on OpenBiblio.* to obiblio_user@localhost identified by 'obiblio_password';`__
* Quit current MySQL session and login as obiblio_user
    * __`quit`__
    * __`mysql -u obiblio_user -p OpenBiblio`__
* Modify database credentials in the database constants file
    * __`nano /var/www/openbiblio/database_constants.php`__
    * USERNAME: _obiblio_user_,  PWD: _obiblio_password_
* 
