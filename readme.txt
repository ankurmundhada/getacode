




------------------------------
Database setting
------------------------------
1) create new user, 

export PATH=$PATH:/usr/local/mysql/bin
mysql --user root --password 
$ root

Local user,  

CREATE USER 'getacodeAdmin'@'localhost' IDENTIFIED BY '!@qwAS45';
GRANT ALL ON *.* TO 'getacodeAdmin'@'localhost';

CREATE USER 'getacodeApp'@'localhost' IDENTIFIED BY '#$we34ANK';
GRANT ALL ON *.* TO 'getacodeApp'@'localhost';

flush privileges;


Create new schema, 
CREATE DATABASE CODE ;
USE CODE;

CREATE TABLE CODE.IFSC (
  IFSC_CODE varchar(15) NOT NULL,
  MICR_CODE varchar(15) NOT NULL,
  BANK varchar(256) NOT NULL,
  BRANCH varchar(256) NOT NULL,
  CONTACT varchar(256) NOT NULL,
  ADDRESS varchar(512) NOT NULL,
  DISTRICT varchar(128) NOT NULL,
  CITY varchar(128) NOT NULL,
  STATE varchar(128) NOT NULL,
  DB_UPDT_TS datetime DEFAULT NULL,
  DB_INST_TS datetime NOT NULL DEFAULT CURRENT_TIMESTAMP,
  PRIMARY KEY (IFSC_CODE));

CREATE TABLE CODE.GROUP (
  GROUP_ID INT NOT NULL AUTO_INCREMENT,
  NAME VARCHAR(45) NOT NULL,
  STATUS VARCHAR(45) NOT NULL DEFAULT 'A',
  DB_UPDT_TS DATETIME NULL,
  DB_INST_TS DATETIME NOT NULL,
  PRIMARY KEY (GROUP_ID),
  UNIQUE INDEX ID_UNIQUE (GROUP_ID ASC));

CREATE TABLE CODE.USER (
  ID INT NOT NULL AUTO_INCREMENT,
  GROUP_ID INT NOT NULL DEFAULT 0,
  USER VARCHAR(45) NOT NULL,
  PASSWORD VARCHAR(45) NOT NULL,
  STATUS CHAR(1) NOT NULL DEFAULT 'A',
  DB_UPDT_TS DATETIME NULL,
  DB_INST_TS DATETIME NULL,
  PRIMARY KEY (ID),
  UNIQUE INDEX ID_UNIQUE (ID ASC));


------------------------------
GIT
------------------------------
git init
git commit -m "first time commit"
git remote add origin https://github.com/ankurmundhada/getacode.git
git pull origin master
git push origin master

to add file chnages to git, 
git commit readme.txt -m "adding GIT commands"
git push origin master

------------------------------
Apache configrations, 
------------------------------
1) Create new vhost file. 
	touch /etc/apache2/vhosts/getacode.in.conf

<VirtualHost *:80>
        DocumentRoot "/Users/ankurmundhada/www/getacode/src"
        ServerName www.getacode.in
        ErrorLog "/Users/ankurmundhada/www/getacode/log/getacode.local-error_log"
        CustomLog "/Users/ankurmundhada/www/getacode/log/getacode.local-access_log" common

        <Directory "/Users/ankurmundhada/www/getacode/src">
                AllowOverride All
                Order allow,deny
                Allow from all
                Require all granted
        </Directory>
</VirtualHost>

2) Verify apachec config file, 
	apachectl configtest
and restart apache server, 
	apachectl restart
check if apache server started...
	ps -ef | grep -i http

2) Add entry in /etc/hosts file.
	
	127.0.0.1	www.getacode.in

3) give read write access to other, 
	cd /Users/ankurmundhada/www/getacode/
	chmod -R a+rw *

