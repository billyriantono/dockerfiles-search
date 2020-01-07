FROM wordpress:latest

# Setup website to send emails
RUN apt update && apt install ssmtp mailutils -y \
    && echo "sendmail_path=$(which sendmail) -i -t" >> /usr/local/etc/php/conf.d/php-sendmail.ini \
    && echo "FromLineOverride=YES" >> /etc/ssmtp/ssmtp.conf

# Use the default production configuration
RUN mv $PHP_INI_DIR/php.ini-production $PHP_INI_DIR/php.ini \
    && pecl config-set php_ini $PHP_INI_DIR/php.ini

# Install memcached
RUN apt install -y libmemcached-dev zlib1g-dev \
    && pecl install memcached \
    && docker-php-ext-enable memcached opcache
