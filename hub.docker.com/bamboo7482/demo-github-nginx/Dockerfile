FROM ubuntu:16.04
MAINTAINER king<king123@gmail.com>
RUN apt-get update -y && \
    apt-get install -y \
    php-fpm php-mysql
VOLUME ["/var/www/html"]
WORKDIR /var/www/html
EXPOSE 9000
CMD ["php-fpm7.0"]
