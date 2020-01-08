# based on custom slim image
FROM mecrawlings/php:7.1-apache

# set working directory
WORKDIR /var/www/localhost/htdocs/

# copy kirby
COPY ./wordpress /var/www/localhost/htdocs/

# set permissions
RUN chown -R apache:apache /var/www/localhost/htdocs/
  # && chmod -R 755 /var/www/localhost/htdocs/thumbs
