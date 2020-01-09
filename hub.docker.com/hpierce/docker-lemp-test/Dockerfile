FROM hpierce/docker-ubuntu-16.04-base
MAINTAINER Hugh Pierce

ENV DEBIAN_FRONTEND=noninteractive
ENV mysql_root_pwd=p@ssw0rd

# Update system & install packages
RUN apt-get install -y nginx php7.0-fpm php7.0-mysql mysql-server

# Setup MySQL
RUN service mysql start && mysqladmin -u root password $mysql_root_pwd && \
    service mysql stop

# Copy data
COPY test_db /var/www/test_db
COPY html /var/www/html
COPY site-default /etc/nginx/sites-enabled/default

# Import database
RUN service mysql start && cd /var/www/test_db && \
    mysql -p$mysql_root_pwd < employees.sql && \
    mysql -p$mysql_root_pwd -t < test_employees_sha.sql && \
    service mysql stop

# Set permissions
RUN chown -R www-data /var/www /var/log/nginx

EXPOSE 80

# Start services
ENTRYPOINT service mysql start && service php7.0-fpm start && \
           service nginx start && /bin/bash

