FROM php:7.2-apache

# Install deps
RUN apt-get update \
    && apt-get -y install git libldap2-dev libpq-dev zlib1g-dev libicu-dev g++

# Configure PHP & Apache 2
RUN docker-php-ext-install ldap pdo pdo_pgsql json intl
RUN a2enmod authnz_ldap
RUN a2dissite 000-default
RUN echo "Listen 8080" >> /etc/apache2/ports.conf

# Download and prepare app
WORKDIR /var/www/html
RUN git clone https://github.com/operasoftware/dns-ui.git .

# Copy default configs
RUN mkdir /var/www/html/install
RUN cp /var/www/html/config/config-sample.ini /var/www/html/install
COPY apache-default.conf /var/www/html/install
RUN chown -R www-data:www-data /var/www/html/


# Set up entrypoint script
RUN rm /usr/local/bin/docker-php-entrypoint
COPY docker-php-entrypoint /usr/local/bin/
RUN chmod 775 /usr/local/bin/docker-php-entrypoint

# Run application
EXPOSE 8080
ENTRYPOINT ["/usr/local/bin/docker-php-entrypoint"]
CMD ["/usr/local/bin/apache2-foreground"]
