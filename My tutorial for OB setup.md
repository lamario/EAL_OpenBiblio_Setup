# EAL_OpenBiblio_Setup
Setup tutorial for OpenBiblio at EAL (you can copy-paste commands)

1. Install a Linux Virtual Machine (e.g. Ubuntu Server)
2. Use Putty - you can copy-paste commands
3. This guide assumes you have root permissions - if not, use the __sudo__ command
4. Once installed, download a LAMP server
    * During instalation: auto install MySQL and Apache2; or
    * for Ubuntu: __`apt-get install lamp-server^`__
5. Download OpenBiblio
    * __`wget http://downloads.sourceforge.net/project/obiblio/OpenBiblio/0.7.2/openbiblio-0.7.2.zip`__
6. Install unzip
    * __`apt-get install unzip`__
7. Unzip openbiblio zip file into your webserver directory
    * __`unzip openbiblio-0.7.2.zip -d /var/www/html`__
8. Start MySQL command line as root
    * __`mysql -u root -p`__
    * enter your MySQL password
9. MySQL commands end with a semicolon ";"
10. Create a new OpenBiblio database
    * __`create database OpenBiblio /*!40100 default character set latin1 */;`__
11. Verify that it worked
    * __`show databases;`__
    * You should see a small table with "OpenBiblio"
12. Create a new MySQL user with priviliges to the OB database
    * user: _obiblio_user_,  password: _obiblio_password_
    * __`grant all privileges on OpenBiblio.* to obiblio_user@localhost identified by 'obiblio_password';`__
13. Quit current MySQL session and login as obiblio_user
    * __`quit`__
    * __`mysql -u obiblio_user -p OpenBiblio`__
14. Modify database credentials in the database constants file
    * __`nano /var/www/html/openbiblio/database_constants.php`__
    * USERNAME: _obiblio_user_,  PWD: _obiblio_password_
    * Exit nano by hitting __"Ctrl+O, Enter, Ctrl+X"__
15. Open the index.php file in your browser to see if everything is working
    * To install a web browser Links: __`apt-get install links`__
    * __`links http://192.168.0.145/openbiblio/install/index.php`__
    * You will most likely see a Mismatch in time and date configuration. Error
    * To close Links browser hit the __"q"__ key and hit Enter
16. Since there is an Error with the time/date, you will need to set the correct time zone
    * __`nano /etc/php5/apache2/php.ini`__
    * Do a search with __"Ctrl+W"__ for __"date.timezone"__ and hit Enter
    * Locate the line that looks like this: __`;date.timezone = `__
    * Uncomment the line by deleting the semicolon at the beginning of the line
    * Add your timezone e.g. __`"Europe/Copenhagen"`__
    * It should look like this: __`date.timezone = "Europe/Copenhagen"`__
    * Now save and exit nano
17. For this change to take effect, restart Apache
    * __`/etc/init.d/apache2 restart`__
18. Security Tip #1 - Remove the Openbiblio/install directory to prevent unauthorized use of install and upgrade tools
    * __`rm -r /var/www/html/openbiblio/install`__
19. Security Tip #2 - Verify that the __"display_errors"__ setting is set to __"Off"__ in the php.ini file
    * Check step no. 16 on how to locate this setting
