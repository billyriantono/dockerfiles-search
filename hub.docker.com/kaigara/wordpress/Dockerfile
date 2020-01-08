FROM wordpress:4.8-php5.6-apache

RUN apt-get update
RUN apt-get install -yy libzip-dev php-pclzip
RUN pecl install zip

# Install Kaigara
RUN curl -sL https://kaigara.org/get | sh
COPY operations /opt/kaigara/operations
COPY resources /etc/kaigara/resources

ENTRYPOINT ["kaigara"]

CMD ["start", "docker-entrypoint.sh", "apache2-foreground"]
