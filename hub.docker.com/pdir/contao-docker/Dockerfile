FROM ubuntu:xenial

ENV DEBIAN_FRONTEND noninteractive
ENV INITRD No
# Set it to a fix version number if you want to run a specific version
ARG CONTAO_VERSION=~4.4

RUN apt-get update
RUN apt-get install -y curl zip unzip
RUN apt-get install -y nginx
RUN apt-get install -y php php-dom php-gd php-curl php-intl php-mbstring php-mysql php-soap
RUN apt-get install -y php-fpm
RUN apt-get install -y supervisor
RUN apt-get install -y mysql-client
RUN apt-get install -y vim rsync git

RUN curl -sS https://getcomposer.org/installer | php && mv composer.phar /usr/local/bin/composer
RUN rm -rf /var/www/html/ && composer create-project contao/managed-edition:$CONTAO_VERSION /var/www/html/

# Link the console cmd
RUN mkdir /var/www/html/bin \
    && ln -s /var/www/html/vendor/bin/contao-console /var/www/html/bin/console \
    && chown -R www-data:www-data /var/www/html/bin/console

# Install Contao Manager
RUN curl -o /var/www/html/web/contao-manager.php -L https://download.contao.org/contao-manager.phar

# Supervisor
RUN mkdir -p /var/log/supervisor /run/php
COPY ./build/supervisord.conf /etc/supervisor/conf.d/supervisord.conf
COPY ./build/nginx.conf /etc/nginx/sites-enabled/default

EXPOSE 80
WORKDIR /var/www/html
HEALTHCHECK CMD curl --fail http://localhost/ || exit 1

CMD ["/usr/bin/supervisord", "-n"]

# Add config, demo and deploy scripts
ADD config /var/www/html/data/config
ADD contao_demo /var/www/html/data/demo
ADD scripts /var/www/html/scripts
RUN chmod -R 0777 /var/www/html/data/
RUN chmod -R 0777 /var/www/html/scripts
RUN chown -R www-data:www-data /var/www/html/data
RUN chown -R www-data:www-data /var/www/html/scripts

#Install dev
RUN chmod +x /var/www/html/scripts/install-dev.php

# Fix permissions
RUN chmod -R 0777 /tmp && chown -R www-data:www-data /tmp
RUN chown -R www-data:www-data /var/www/html