FROM php:5-apache

RUN apt-get update -y && \
	apt-get install -y git --no-install-recommends && \
	rm -r /var/lib/apt/lists/*

RUN curl -O https://getcomposer.org/composer.phar && chmod +x composer.phar && mv composer.phar /usr/local/bin/composer

# RUN git clone https://github.com/clickalicious/phpmemadmin.git /app
RUN echo '\
{\n\
    "require": {\n\
        "clickalicious/phpmemadmin": "~0.3"\n\
    },\n\
    "scripts": {\n\
    	"post-autoload-dump": [\n\
        	"Clickalicious\\\\PhpMemAdmin\\\\Installer::postInstall"\n\
    	]\n\
    }\n\
}' > composer.json

RUN echo '1\nY' > /auto-response && composer install --no-dev < /auto-response && rm /auto-response

RUN rm /etc/apache2/sites-enabled/000-default.conf && echo '\
<VirtualHost *:80>\n\
    ServerAdmin webmaster@localhost\n\
    ErrorLog ${APACHE_LOG_DIR}/error.log\n\
    CustomLog ${APACHE_LOG_DIR}/access.log combined\n\
\n\
    DocumentRoot /var/www/html/web\n\
    <Directory /var/www/html/web>\n\
        Options Indexes FollowSymLinks Includes ExecCGI\n\
        AllowOverride All\n\
        Order allow,deny\n\
        Allow from all\n\
        DirectoryIndex index.php\n\
    </Directory>\n\
</VirtualHost>' > /etc/apache2/sites-enabled/000-default.conf

ENV PHP_TIMEZONE "UTC"
ENV PHPMEMADMIN_USERNAME "username"
ENV PHPMEMADMIN_PASSWORD "password"

# A list of hosts separated by a ";", example: MEMCACHE_HOSTS="127.0.0.1:11211;127.0.0.1:11212"
ENV MEMCACHE_HOSTS "127.0.0.1:11211"

COPY .config.dist /var/www/html/app/.config.dist

RUN echo '\
#!/bin/bash\n\
echo "[PHP]\ndate.timezone = \"${PHP_TIMEZONE}\"" > /usr/local/etc/php/conf.d/timezone.ini\n\
\n\
cp /var/www/html/app/.config.dist /var/www/html/app/.config\n\
PREPARED_HOSTS=""\n\
OIFS=$IFS\n\
IFS=";"\n\
for MEMCACHE_HOST in $MEMCACHE_HOSTS; do\n\
    HOST=`echo $MEMCACHE_HOST | grep : | cut -d: -f1`\n\
    PORT=`echo $MEMCACHE_HOST | grep : | cut -d: -f2`\n\
    JSON_CFG="{\"host\": \"$HOST\",\"port\": $PORT}"\n\
    if [ -z "$PREPARED_HOSTS" ]; then\n\
        PREPARED_HOSTS="$JSON_CFG"\n\
    else\n\
        PREPARED_HOSTS="$PREPARED_HOSTS,$JSON_CFG"\n\
    fi\n\
done\n\
IFS=$OIFS\n\
sed -i "s/PHPMEMADMIN_USERNAME/${PHPMEMADMIN_USERNAME}/" /var/www/html/app/.config\n\
sed -i "s/PHPMEMADMIN_PASSWORD/${PHPMEMADMIN_PASSWORD}/" /var/www/html/app/.config\n\
sed -i "s/PHPMEMADMIN_HOSTS/${PREPARED_HOSTS}/" /var/www/html/app/.config\n\
apache2-foreground' > /entrypoint.sh && chmod +x /entrypoint.sh

CMD ["/entrypoint.sh"]
