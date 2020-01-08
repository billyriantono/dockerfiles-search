FROM chunhsin/php-5.4:latest
RUN yum -y --enablerepo=remi install php-mysql
RUN composer create-project phpmyadmin/phpmyadmin /var/www/html/ dev-STABLE

RUN cp /var/www/html/config.sample.inc.php /var/www/html/config.inc.php

# Modify $cfg['Servers'][$i]['host'] = "localhost";
# TO     $cfg['Servers'][$i]['host'] = getenv('MYSQL_HOST');

RUN sed -i "s/'localhost'/getenv('MYSQL_HOST')/g" /var/www/html/config.inc.php

COPY docker-entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]

VOLUME ["/var/log/httpd","/var/www/html"]

CMD /sbin/init