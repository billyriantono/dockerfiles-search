FROM fedora

RUN yum update -y
RUN yum install -y php php-pdo php-mysql php-pgsql php-mbstring php-mcrypt psmisc sqlite

RUN echo -e '<VirtualHost *:80> \n DocumentRoot /var/www/html/public \n <Directory "/var/www/html/public"> \n AllowOverride All \n Require all granted \n </Directory> \n </VirtualHost>' > /etc/httpd/conf.d/vhost.conf
RUN echo 'date.timezone = "America/New_York"' > /etc/php.d/zz_timezone.ini

VOLUME  ["/var/www/html"]
EXPOSE 80

ENTRYPOINT ["httpd", "-D", "FOREGROUND"]
