####################################
# PHPDocker.io PHP 7.0 / FPM image #
####################################

FROM phpdockerio/php7-cli
MAINTAINER Gabor Huszak <huszy@bigfish.hu>

# Install FPM
RUN apt-get update \
    && apt-get -y --no-install-recommends install php7.0-fpm php7.0-pgsql php-pear php7.0-dev php7.0-gd libcurl4-openssl-dev pkg-config libssl-dev make \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/*

RUN pecl install mongodb
RUN echo "extension=mongodb.so" > /etc/php/7.0/mods-available/mongodb.ini
RUN ln -s /etc/php/7.0/mods-available/mongodb.ini /etc/php/7.0/fpm/conf.d/10-mongodb.ini
RUN ln -s /etc/php/7.0/mods-available/mongodb.ini /etc/php/7.0/cli/conf.d/10-mongodb.ini
RUN phpenmod pgsql

# Configure FPM to run properly on docker
RUN sed -i "/listen = .*/c\listen = [::]:9000" /etc/php/7.0/fpm/pool.d/www.conf \
    && sed -i "/;access.log = .*/c\access.log = /proc/self/fd/2" /etc/php/7.0/fpm/pool.d/www.conf \
    && sed -i "/;clear_env = .*/c\clear_env = no" /etc/php/7.0/fpm/pool.d/www.conf \
    && sed -i "/;catch_workers_output = .*/c\catch_workers_output = yes" /etc/php/7.0/fpm/pool.d/www.conf \
    && sed -i "/pid = .*/c\;pid = /run/php/php7.0-fpm.pid" /etc/php/7.0/fpm/php-fpm.conf \
    && sed -i "/;daemonize = .*/c\daemonize = no" /etc/php/7.0/fpm/php-fpm.conf \
    && sed -i "/error_log = .*/c\error_log = /proc/self/fd/2" /etc/php/7.0/fpm/php-fpm.conf \
    && usermod -u 1000 www-data

# The following runs FPM and removes all its extraneous log output on top of what your app outputs to stdout
CMD /usr/sbin/php-fpm7.0 -F -O 2>&1 | sed -u 's,.*: \"\(.*\)$,\1,'| sed -u 's,"$,,' 1>&1

# Open up fcgi port
EXPOSE 9000