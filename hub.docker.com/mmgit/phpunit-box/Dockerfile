FROM ubuntu:16.04

MAINTAINER mm-git

RUN apt-get update -y
RUN apt-get upgrade -y
RUN apt-get install -y -q sudo curl unzip git
RUN apt-get install -y -q php-fpm php-pgsql php-xml php-mbstring
RUN apt-get install -y -q ruby

RUN sed -i -e "s|;date.timezone =|date.timezone =\"Asia/Tokyo\"|g" /etc/php/7.0/fpm/php.ini
RUN sed -i -e "s|;extension=php_openssl.dll|extension=php_openssl.so|g" /etc/php/7.0/fpm/php.ini
RUN sed -i -e "s|;extension=php_pdo_pgsql.dll|extension=php_pdo_pgsql.so|g" /etc/php/7.0/fpm/php.ini
RUN sed -i -e "s|upload_max_filesize = 2M|upload_max_filesize = 1G|g" /etc/php/7.0/cli/php.ini
RUN sed -i -e "s|post_max_size = 8M|post_max_size = 1G|g" /etc/php/7.0/cli/php.ini

RUN apt-get install -y -q postgresql=9.5+173
COPY pg_hba.conf /etc/postgresql/9.5/main/

RUN curl -sS https://getcomposer.org/installer | sudo php -- --install-dir=/usr/local/bin --filename=composer
