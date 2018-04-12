
Here's the resulting documentation for our process for deployment. We'll try to add a good amount of detail to make the steps clear.


--------------------------------------------


**Part 1**

**Updating Ubuntu:**

1. sudo apt-get update

2. sudo apt-get upgrade

3. sudo apt-get dist-upgrade

* The above three steps were successful and we didn't run into any prompts or problems.


--------------------------------------------


**Part 2**

**Installing Apache:**

4. sudo apt-get install apache2 apache2-utils
// now you will want to make sure apache2 is active and running

5. systemctl status apache2
// if it is not running, enter this command

6. sudo systemctl start apache2
//then run this command to make sure Apache2 runs automatically after reboot

7. sudo systemctl enable apache2
// Let's test if its working. Enter localhost into the web address bar. It should show as the image below.

8. sudo chown www-data /var/www/html/ -R

* The above five steps were successful and we moved on to the next.


--------------------------------------------


**Part 3**

**Installing MariaDB:**

9. sudo apt-get install mariadb-server mariadb-client

10. systemctl status mysql

// if it is not active, you will want to use systemctl again and enable it to run automatically after reboot.

11. sudo systemctl start mysql

12. sudo systemctl enable mysql

// We can now set security for mariadb, read the prompts and carefully select password and settings.

13. sudo mysql_secure_installation

* The above five steps worked great, and we're able to move onto to the next part installing PHP.


--------------------------------------------


**Part 4**

**Installing PHP:**

14. sudo apt-get install php7.0-fpm php7.0-mysql php7.0-common php7.0-gd php7.0-json php7.0-cli php7.0-curl libapache2-mod-php7.0 php-xml

15. sudo apt install php-mbstring php-json php-mysql php-curl php-intl php-gd texlive

16. sudo apt-get install curl php5-cli git

// We'll skip over the php5 command since it clash with php7

17. sudo apt-get install curl php-cli php-mbstring git unzip

18. sudo a2enmod php7.0

19. sudo systemctl restart apache2

// Enable and restart Apache worked fine

* The PHP installation worked decently


--------------------------------------------


**Part 5**

**Downloading and extracting Mediawiki:**

20. cd /tmp/

21. wget https://releases.wikimedia.org/mediawiki/1.30/mediawiki-1.30.0.targ.gz

22. tar -xyzf /tmp/mediawiki-*.tar.gz

23. sudo mkdir /var/lib/mediawiki

24. sudo mv mediawiki-*/* /var/lib/mediawiki

* The downloading and extracting worked well


-----------------------------------------------


**Part 6**

**Making link and extra installation steps:**

25. mv core mediawiki

// Renaming folder

26. sudo mv mediawiki /var/lib

Moving mediawiki

27. cd /var/lib

28. ls

29. cd /var/www/html

30. sudo ln -s /var/lib/mediawiki mediawiki

31. ls

32. sudo apt install composer

33. cd /var/lib/mediawiki

34. sudo composer install --no-dev

35. sudo chown www-data:www-data /var/lib/mediawiki/ -R

// For the above step we changed the /var/www to /var/lib

* The above steps for creating the folder and links worked well, for step 34 we added sudo because we needed those permissions.


--------------------------------------------


**Part 7**

**Creating the database:**

36. sudo mysql -u root -p

// We used sudo permissions for above

37. CREATE DATABASE Wikinet;

// For the database above we changed its name to Wikinet

38. GRANT ALL PRIVILEGES ON Wikinet.* TO 'klor0610'@'localhost' IDENTIFIED BY '(password here)';

39. flush privileges;

40. exit;

* The database creation worked great, on to the next.


-------------------------------------------


**Part 8**

**Final steps for installation:**

// For the step below we configured the following file like so..

41. sudo nano /etc/apache2/sites-available/mediawiki.conf

// <VirtualHost *:80>

//    ServerAdmin admin@your-domain.com

//    DocumentRoot /var/www//mediawiki/

//    ServerName wiki.your-domain.com

//

//    <Directory /var/www/html/mediawiki/>

//        Options FollowSymLinks

//        AllowOverride All

//        Order allow,deny

//        allow from all

//    </Directory>

//

//    ErrorLog /var/log/apache2/your-domain.com-error_log

//    CustomLog /var/log/apache2/your-domain.com-access_log common

// </VirtualHost>

42. sudo a2ensite mediawiki.conf

43. sudo systemctl reload apache2

44. sudo apt-get install php7.2

// We installed php7.2 to fix an issue with packages

* ( )


-----------------------------------------


**Part 9 Final**

**Conclusion for installation documentation:**

* ( )

