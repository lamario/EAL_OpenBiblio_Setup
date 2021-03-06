# EAL_OpenBiblio_Setup
### Setup tutorial for OpenBiblio at EAL (you can copy-paste commands)

1. Install a Linux Virtual Machine (e.g. Ubuntu Server) 
___
2. Use Putty - you can copy-paste commands
___
3. This guide assumes you have root permissions - if not, use the __sudo__ command
___
4. Once installed, download a LAMP server
    * During instalation: auto install MySQL and Apache2; or
    * for Ubuntu: __`apt-get install lamp-server^`__
___
5. Download OpenBiblio
    * __`wget http://downloads.sourceforge.net/project/obiblio/OpenBiblio/0.7.2/openbiblio-0.7.2.zip`__
___
6. Install unzip
    * __`apt-get install unzip`__
___
7. Unzip openbiblio zip file into your webserver directory
    * __`unzip openbiblio-0.7.2.zip -d /var/www/html`__
___
8. Export the current database of OpenBiblio
    * You will most likely use MyPhpAdmin
___
9. Move backup file to the new VM
___
10. Import a backup of OpenBiblio database
    * __`mysql -u root -p < backup.sql`__
    * enter your MySQL password
___
11. Verify that it worked
    * MySQL commands end with a semicolon ";"
    * __`show databases;`__
    * You should see a small table with "OpenBiblio"
___
12. Create a new MySQL user with priviliges to the OB database
    * user: _obiblio_user_,  password: _obiblio_password_
    * __`grant all privileges on OpenBiblio.* to obiblio_user@localhost identified by 'obiblio_password';`__
___
13. Quit current MySQL session and try login as obiblio_user
    * __`quit;`__
    * __`mysql -u obiblio_user -p OpenBiblio`__
    * If it works, quit again
___
14. Modify database credentials in the database constants file
    * __`nano /var/www/html/openbiblio/database_constants.php`__
    * USERNAME: _obiblio_user_,  PWD: _obiblio_password_
    * Exit nano by hitting __"Ctrl+O, Enter, Ctrl+X"__
___
15. Open the index.php file in your browser to see if everything is working
    * To install a web browser Links: __`apt-get install links`__
    * __`links http://192.168.0.145/openbiblio/install/index.php`__
    * You will most likely see a Mismatch in time and date configuration. Error
    * To close Links browser hit the __"q"__ key and hit Enter
___
16. Since there is an Error with the time/date, you will need to set the correct time zone
    * __`nano /etc/php5/apache2/php.ini`__
    * Do a search with __"Ctrl+W"__ for __"date.timezone"__ and hit Enter
    * Locate the line that looks like this: __`;date.timezone = `__
    * Uncomment the line by deleting the semicolon at the beginning of the line
    * Add your timezone e.g. __`"Europe/Copenhagen"`__
    * It should look like this: __`date.timezone = "Europe/Copenhagen"`__
    * Now save and exit nano
___
17. For this change to take effect, restart Apache
    * __`/etc/init.d/apache2 restart`__
___
18. Security Tip #1 - Remove the Openbiblio/install directory to prevent unauthorized use of install and upgrade tools
    * __`rm -r /var/www/html/openbiblio/install`__
___
19. Security Tip #2 - Verify that the __"display_errors"__ setting is set to __"Off"__ in the php.ini file
    * Check step no. 16 on how to locate this setting
___
20. Security Tip #3 - Remove the Backup.sql file to prevent any unauthorized access to it
    * __`rm -r /home/user/backup.sql`__


[To see the original guide click here.](http://openbiblio.sint-godelieve-instituut.be/install_instructions.html "Original Guide for OpenBilbio")