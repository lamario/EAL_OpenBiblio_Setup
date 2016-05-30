# How to restore OB



# Note to self - How to change Apache2 root dir
+ You need to edit two config files (Vim or Nano)

+ First file: `/etc/apache2/sites-available/000-default.conf`
+ * find `DocumentRoot /var/www/html` and replace the path
+ Second file: `/etc/apache2/apache2.conf`
+ find ```<Directory /var/www/html/>

Options Indexes FollowSymLinks

AllowOverride None

Require all granted

</Directory>``` and replace the path
