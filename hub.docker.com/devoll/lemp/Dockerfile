
FROM debian:latest
MAINTAINER Pavel Nikitaev <devoll@devoll.ru>

# Install packages
RUN apt-get update
RUN apt-get -y install nginx mysql-server php5-fpm php5-common supervisor pwgen

# Add config
COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf
COPY my.cnf /etc/mysql/conf.d/

COPY nginx-default.conf /etc/nginx/sites-available/default
#COPY php-fpm-default.conf /etc/php5/fpm/pool.d/www.conf

# Remove pre-installed database
RUN rm -rf /var/lib/mysql/*

# Remove preinstalled www-files
RUN rm -rf /var/www
RUN mkdir /var/www

# Copy default page
COPY index.php /var/www/

RUN chown -R www-data:www-data /var/www
RUN chmod -R 0755 /var/www

# Change root password
COPY bootstrap.sh /bootstrap.sh
RUN chmod +x /bootstrap.sh

# Open ports
EXPOSE 80 3306

# Start services
CMD ["/bootstrap.sh"]
