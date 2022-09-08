# HW1-CSE135

Team members:
Duc Pham
Trung Tin Vo
Kim Khoa Nguyen

Website:
https://www.cse135vn.site/

Grader account: grader
Password: 1234

1.  Details of Github auto deploy setup
    -----In the server-----
    We first create repository for the server in root site, called repo, by the following commands:
    cd /var mkdir repo && cd repo mkdir site.git && cd site.git git init –bare
    Inside hooks folder, create post-receive file
    cd /hooks
    touch post-receive
    Implement some script which tells server need to do when we do git push:
    #!/bin/sh
    git --work-tree=/var/www/cse135vn.site/public_html --git-dir=/var/repo/site.git checkout –f
    Set execute permission for file post-receive
    chmod +x post-receive
    -----In local machine-----
    Create a repository (in case you don’t have one)
    cd /my/workspace mkdir HW1-CSE135 && cd HW1-CSE135 git init
    Configure remote path of our repository
    git remote add origin ssh://toan95dn@164.92.44.173/var/repo/site.git
    Check all remote path of our repository by using command
    git remote – v
    There should be 2 remote paths for push (one is for github, one is for server)
    Make a necessary change in our code, then using some git commands to push code to both server and github
    git add . git commit -m "initial commit"
    git push origin main
    now codes is pushed to github and also updated in the server.
2.  Username/password info for logging into the site
    Username: grader
    Password: 1234
3.  Summary of changes to HTML file in DevTools after compression
    After compression, we can look at the network tab and see the "Content-Encoding" type is "gzip"
    Also, we can check gzip compression by using online tool to make sure such as
    https://www.giftofspeed.com/gzip-test/
4.  Summary of removing 'server' header
    We remove the server header using the "libapache2-mod-security2", after install the library, we
    put this into the config file of Apache 2
    <IfModule mod_security2.c>
    SecServerSignature "CSE135VN Server"
    </IfModule>
    Finally, we restart the server and make request to the website to check if the server name was changed
5.  Extra credit: Analytics configuration
    Website: matomo.cse135vn.site
    Account: t8vo
    Password: greater1234

    Detail of installing Matomo with Apache

    1.  Download Matomo by following commands:
        sudo wget https://builds.matomo.org/matomo-latest.zip
        sudo apt install unzip
        sudo mkdir -p /var/www/
        sudo unzip matomo-latest.zip -d /var/www/
        sudo chown www-data:www-data /var/www/matomo/ -R
    2.  Create a database MySQL by following commands:
        sudo mysql
        create database matomo;
        create user toan95dn@localhost identified by 'password';
        grant all privileges on matomo.\* to toan95dn@localhost;
        flush privileges;
        exit;
    3.  Create Apache
        sudo nano /etc/apache2/sites-available/matomo.conf
        Change .conf file like below
        <VirtualHost \*:80>
        ServerAdmin webmaster@localhost
        ServerName matomo.cse135vn.site
        DocumentRoot /var/www/matomo/

                 <Directory /var/www/matomo>
                 DirectoryIndex index.php
                 Options FollowSymLinks
                 AllowOverride All
                 Require all granted
                 </Directory>

                 <Files "console">
                 Options None
                 Require all denied
                 </Files>

                 <Directory /var/www/matomo/misc/user>
                 Options None
                 Require all granted
                 </Directory>

                 <Directory /var/www/matomo/misc>
                 Options None
                 Require all denied
                 </Directory>

                 <Directory /var/www/matomo/vendor>
                 Options None
                 Require all denied
                 </Directory>

                 ErrorLog $APACHE_LOG_DIR/matomo_error.log
                 CustomLog $APACHE_LOG_DIR/matomo_access.log combined

             </VirtualHost>

        then, enable virtual host
        sudo a2ensite matomo.conf
        sudo systemctl reload apache2

    4.  Install and enable PHP Modules
        sudo apt install php-imagick php7.4-common php7.4-gd php7.4-json php7.4-curl php7.4-zip php7.4-xml php7.4-mbstring php7.4-bz2 php7.4-intl
    5.  Install Matomo on our browser: https://matomo.cse135vn.site/
