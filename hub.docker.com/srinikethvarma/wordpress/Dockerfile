FROM ubuntu:18.04

# Install Apache2
ARG DEBIAN_FRONTEND=noninteractive

RUN apt-get update
RUN apt-get install -y apache2
# Install required php modules
RUN apt-get install -y php libapache2-mod-php php-mysql php-pgsql
RUN apt-get install -y php-curl php-gd php-xml php-mbstring  php-xmlrpc php-zip php-soap php-intl

ENV APACHE_RUN_USER="www-data" \
    APACHE_RUN_GROUP="www-data" \
    APACHE_LOG_DIR="/var/log/apache2" \
    APACHE_RUN_DIR="/var/run/apache2"

#RUN mkdir /var/run/apache2

RUN rm /var/www/html/index.html
COPY wordpress-config/html /var/www/html

EXPOSE 80 443

ENTRYPOINT ["/usr/sbin/apache2"]
CMD ["-D", "FOREGROUND"]