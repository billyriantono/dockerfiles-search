FROM alpine:3.9
LABEL author="Serge NOEL <serge.noel@easylinux.fr>"

RUN apk add --no-cache php7-apache2 phpmyadmin \
    && ln -s /dev/stdout /var/log/apache2/access.log \
    && ln -s /dev/stdin  /var/log/apache2/error.log \

    && chown -R apache: /etc/phpmyadmin \

    && rm /etc/apache2/conf.d/phpmyadmin.conf \
    && sed -i "s|/var/www/localhost/htdocs|/usr/share/webapps/phpmyadmin/|g" /etc/apache2/httpd.conf \
    && sed -i "s|//$cfg['DefaultLang'] = 'de';|$cfg['DefaultLang'] = 'fr';|g" /etc/phpmyadmin/config.inc.php \ 
    && sed -i "s/localhost/MARIADB/g" /etc/phpmyadmin/config.inc.php 

COPY Files/ /

ENV DBHOST=MariaDB

EXPOSE 80

CMD /usr/local/bin/launch-phpmyadmin


