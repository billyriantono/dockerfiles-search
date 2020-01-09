FROM debian:stretch-slim

ENV APACHE_APPLICATION_ROOT /var/www/
ENV APACHE_CONFDIR /etc/apache2
ENV APACHE_DOCUMENT_ROOT /var/www/html
ENV APACHE_FCGI_HOSTNAME php-fpm
ENV APACHE_FCGI_PORT 9000
ENV APACHE_LOG_DIR /var/log/apache2
ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_SERVER_ADMIN webmaster@localhost
ENV APACHE_SERVER_NAME localhost

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        apache2>=2.4.39 \
        curl \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

RUN { \
    echo "ServerName \${APACHE_SERVER_NAME}"; \
    echo; \
    echo "<FilesMatch \\.php$>"; \
    echo "  SetHandler proxy:fcgi://\${APACHE_FCGI_HOSTNAME}:\${APACHE_FCGI_PORT}"; \
    echo "</FilesMatch>"; \
    echo; \
    echo "DirectoryIndex disabled"; \
    echo "DirectoryIndex index.php index.html"; \
    echo; \
    echo "<Directory \${APACHE_APPLICATION_ROOT}>"; \
    echo "  Options FollowSymLinks"; \
    echo "  AllowOverride All"; \
    echo "  Require all granted"; \
    echo "</Directory>"; \
} | tee "${APACHE_CONFDIR}/conf-available/docker-php.conf"

RUN { \
    echo "<VirtualHost *:80>"; \
    echo "  ServerAdmin \${APACHE_SERVER_ADMIN}"; \
    echo; \
    echo "  DocumentRoot \${APACHE_DOCUMENT_ROOT}"; \
    echo; \
    echo "  ErrorLog \${APACHE_LOG_DIR}/error.log"; \
    echo "  CustomLog \${APACHE_LOG_DIR}/access.log combined"; \
    echo "</VirtualHost>"; \
} | tee "${APACHE_CONFDIR}/sites-available/000-default.conf"

RUN a2enconf docker-php \
    && a2enmod proxy_fcgi rewrite

EXPOSE 80

CMD [ "/usr/sbin/apache2ctl", "-DFOREGROUND" ]
