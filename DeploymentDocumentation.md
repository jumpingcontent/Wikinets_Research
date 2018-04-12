
Here's the resulting documentation for our process for deployment. We'll try to add a good amount of detail to make the steps clear.




Updating Ubuntu:

1. sudo apt-get update

2 sudo apt-get upgrade

3. sudo apt-get dist-upgrade

--------------------------------------------

The above three steps were successful and we didn't run into any prompts or problems.




4. sudo apt-get install apache2 apache2-utils
// now you will want to make sure apache2 is active and running

5. systemctl status apache2
// if it is not running, enter this command

6. sudo systemctl start apache2
//then run this command to make sure Apache2 runs automatically after reboot

7. sudo systemctl enable apache2
// Let's test if its working. Enter localhost into the web address bar. It should show as the image below.

------------------------------------------------

The above four steps were successful and we moved on to the next.




8. sudo chown www-data /var/www/html/ -R

---------------------------------------------

This step worked fine too




9. sudo apt-get install mariadb-server mariadb-client

10. systemctl status mysql

// if it is not active, you will want to use systemctl again and enable it to run automatically after reboot.

11. sudo systemctl start mysql

12. sudo systemctl enable mysql

// We can now set security for mariadb, read the prompts and carefully select password and settings.

13. sudo mysql_secure_installation

----------------------------------

The above five steps worked great, and we're able to move onto to the next part installing PHP.




14. sudo apt-get install php7.0-fpm php7.0-mysql php7.0-common php7.0-gd php7.0-json php7.0-cli php7.0-curl libapache2-mod-php7.0 php-xml

15. sudo apt install php-mbstring php-json php-mysql php-curl php-intl php-gd texlive

16. sudo apt-get install curl php5-cli git

17. sudo apt-get install curl php-cli php-mbstring git unzip

// Enable and restart Apache

18. sudo a2enmod php7.0

19. sudo systemctl restart apache2

--------------------------------------------
