FROM studionone/nginx-v8js-php:7.1

ENV TERM xterm-256color

RUN apt-get update && \
    apt-get install -y \
    dialog \
    mysql-client \
    php7.1-mysql \
    php-xml \
    php-curl

RUN mkdir -p /run/php /var/run/php /var/www
RUN mkdir -p /var/www/var/cache /var/www/var/logs
RUN sed -i -e "s/^;clear_env = no/clear_env = no/g" /etc/php/7.1/fpm/pool.d/www.conf

# Install wkhtmltopdf
RUN apt-get update && apt-get install -y wkhtmltopdf \
    && wget https://github.com/wkhtmltopdf/wkhtmltopdf/releases/download/0.12.3/wkhtmltox-0.12.3_linux-generic-amd64.tar.xz \
    && tar -xJf wkhtmltox-0.12.3_linux-generic-amd64.tar.xz \
    && mv wkhtmltox/bin/wkhtmltopdf /usr/bin \
    && rm -rf wkhtmltox wkhtmltox-0.12.3_linux-generic-amd64.tar.xz

# Install Node.js v8.9.4 LTS
WORKDIR /opt
RUN wget https://nodejs.org/download/release/v8.9.4/node-v8.9.4-linux-x64.tar.gz \
    && tar -zxvf node-v8.9.4-linux-x64.tar.gz \
    && ln -s /opt/node-v8.9.4-linux-x64/bin/node /usr/local/bin/node && ln -s /opt/node-v8.9.4-linux-x64/bin/npm /usr/local/bin/npm

# Install Composer
RUN wget -O /tmp/composer.phar https://getcomposer.org/composer.phar \
    && cp /tmp/composer.phar /usr/local/bin/composer \
    && chmod +x /usr/local/bin/composer \
    && composer self-update && composer global require hirak/prestissimo

# Add default page for testing nginx
COPY var/www /var/www

WORKDIR /var/www

EXPOSE 80

COPY start.sh /start.sh
RUN chmod +x /start.sh
ENTRYPOINT ["/start.sh"]
