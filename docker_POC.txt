*)https://github.com/jayaprakashdeav/docker_hands_on
*)run tomcate image in server

use below public IP to access the apache tomcat
http://54.173.14.209:8080  ----> (check Dockerfile.../webapps/ROOT.war)
http://54.173.14.209:8080/onlinebookstore-0.0.1-SNAPSHOT/  ----> (check Dockerfile.../webapps/onlinebookstore-0.0.1-SNAPSHOT.war)

---------------------------------------------------------------------------------------------------------------------------------------------------------

*)apt install apache2
*)add beloe inside the virtaul block

cd /etc/apache2/sites-available
vi vi 000-default.conf



	ProxyPreserveHost On
        ProxyRequests Off
        ServerName www.onlinebookstore100.com
        ServerAlias onlinebookstore100.com
        ProxyPass / http://54.173.14.209:8080/onlinebookstore-0.0.1-SNAPSHOT/
        ProxyPassReverse / http://54.173.14.209:8080/onlinebookstore-0.0.1-SNAPSHOT/

sudo a2enmod proxy && sudo a2enmod proxy_http && sudo service apache2 restart




*) after adding above view it ll show Full view or example 000-default.conf like below

<VirtualHost *:80>
        # The ServerName directive sets the request scheme, hostname and port that
        # the server uses to identify itself. This is used when creating
        # redirection URLs. In the context of virtual hosts, the ServerName
        # specifies what hostname must appear in the request's Host: header to
        # match this virtual host. For the default virtual host (this file) this
        # value is not decisive as it is used as a last resort host regardless.
        # However, you must set it for any further virtual host explicitly.
        #ServerName www.example.com

        ServerAdmin webmaster@localhost
        DocumentRoot /var/www/html
         ProxyPreserveHost On
        ProxyRequests Off
        ServerName www.onlinebookstore100.com
        ServerAlias onlinebookstore100.com
        ProxyPass / http://54.173.14.209:8080/onlinebookstore-0.0.1-SNAPSHOT/
        ProxyPassReverse / http://54.173.14.209:8080/onlinebookstore-0.0.1-SNAPSHOT/
        # Available loglevels: trace8, ..., trace1, debug, info, notice, warn,
        # error, crit, alert, emerg.
        # It is also possible to configure the loglevel for particular
        # modules, e.g.
        #LogLevel info ssl:warn

        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined

        # For most configuration files from conf-available/, which are
        # enabled or disabled at a global level, it is possible to
        # include a line for only one particular virtual host. For example the
        # following line enables the CGI configuration for this host only
        # after it has been globally disabled with "a2disconf".
        #Include conf-available/serve-cgi-bin.conf
</VirtualHost>

*)In AWS server
*)sudo vi /etc/hosts
*)127.0.0.1 www.onlinebookstore100.com
*)In Laptop C:\Windows\System32\drivers\etc\
*)open with notepad++ in admin mode hosts
*)54.173.14.209 www.onlinebookstore100.com (54.173.14.209 -> public IP of ec2 server)

