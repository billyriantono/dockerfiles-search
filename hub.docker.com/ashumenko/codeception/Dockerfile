#Download base image ubuntu 16.04
FROM ubuntu:latest
 
# Update Software repository
RUN apt-get update
 
# Install nginx, php-fpm and supervisord from ubuntu repository
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y git php php-phar php-iconv curl php-curl php-mbstring php-dom sendmail
RUN curl -LsS https://codeception.com/codecept.phar -o /usr/local/bin/codecept
RUN chmod a+x /usr/local/bin/codecept

