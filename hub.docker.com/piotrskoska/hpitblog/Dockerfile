FROM php:apache-stretch
ADD https://github.com/picocms/Pico/releases/download/v2.0.4/pico-release-v2.0.4.tar.gz /var/www/html
RUN cd /var/www/html && tar -xzf pico-release-v2.0.4.tar.gz && rm pico-release-v2.0.4.tar.gz && \
    chown -R www-data:www-data /var/www/html && \
    chmod -R 755 /var/www/html && \
    a2enmod ssl && \
    a2ensite 000-default.conf && \
    a2ensite default-ssl.conf && \
    a2enmod rewrite
EXPOSE 80
# Run apache2. # Materiał YouTube
CMD apachectl -D FOREGROUND
