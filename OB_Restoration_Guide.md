# How to restore OB
This guide will take throught the simple process of restoring OpenBiblio in the cases of server failure, database crash or just moving it to a new machine. In this example, I will focus on the "moving from an old to a new machine" scenario, but the general thoughts can be adapted for other ones as well.

## Part ONE - Move important data
By important data, I mean the MySQL database, OpenBiblio itself and scripts what will do most of the work for you. To do this, there are multiple ways, but the two most SAFE and RECOMMENDED are: Git Clone and SCP. Also, this guide is made with Linux servers in mind only.

### Git
This method can only be used, when your old machine - or any machine containing this data e.g. backup server - had this data in a Git Repositary.
On the "new" machine:
1. Install Git (NOT GitHub) on the new machine
  1. `sudo apt-get install git`
2. Edit the git config
  1. Git wont let you commit without you telling it who you are:
  `git config --global user.email johndoe@example.com` and `git config --global user.name "John Doe"`
3. Make sure both new and old machines are on the same network
  1. Write down, what IP address does the old machine have (e.g. 192.168.1.50)
  `ifconfig` on the "old" machine
4. CLONE
  1. Navigate to your home folder - this is how the scripts were made, you can change them before running.
  1. `git clone ssh://user@192.168.1.50/path/to/repositary.git`
  2. Clonining is automatic after typing in the users password

### SCP
The Secure Copy protocol is based on SSH (Secure Shell Protocol), so the two machines will need to be on the same network, with known IP addresses e.g. 192.168.1.50. This method should be used only when you dont have your data / scripts in a Git Repository. 

On the "old" machine:
1. Tar your files
  1. `tar cfzv files.tar.gz /path/to/files`

On the "new" machine:
2. Navigate to your Home directory
  1. `cd $HOME` or `cd /home/user/`
3. COPY
  1. `scp user@192.168.1.50/path/to/files.tar.gz .`
4. Untar the zip
  1. `tar xfv files.tar.gz`
  2. After this, you should have copied your files successfully



# Note to self - How to change Apache2 root dir
+ You need to edit two config files (Vim or Nano)

+ First file: `/etc/apache2/sites-available/000-default.conf`
  + find `DocumentRoot /var/www/html` and replace the path

+ Second file: `/etc/apache2/apache2.conf`
  + find `<Directory /var/www/html/>` and replace the path

+ After saving changes, restart apache2: `sudo service apache2 restart`
