# Nginx / PHP webserver for development

FROM juhasz/nginx-php:latest
MAINTAINER Márton Juhász <m@juhaszmarton.hu>

# Enable phusion/baseimage default insecure SSH key.
# So this image useable only for development purposes.
RUN /usr/sbin/enable_insecure_key

RUN add-apt-repository ppa:git-core/ppa

RUN apt-get update && apt-get install -y php5-xdebug mysql-client git

COPY etc/php5/fpm/php.ini /etc/php5/fpm/php.ini
COPY etc/php5/fpm/conf.d/20-xdebug.ini /etc/php5/fpm/conf.d/20-xdebug.ini
