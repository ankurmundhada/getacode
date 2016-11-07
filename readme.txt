







GIT, 
git init
git commit -m "first time commit"
git remote add origin https://github.com/ankurmundhada/getacode.git
git pull origin master
git push origin master
git push -u origin master




Apache configrations, 
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

