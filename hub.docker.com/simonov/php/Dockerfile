FROM ubuntu:16.04

MAINTAINER "Andrew Simonov <simonov@scand.com>"

RUN apt-get update \
    && apt-get install -y --no-install-recommends nano curl software-properties-common \
    && LC_ALL=C.UTF-8 add-apt-repository ppa:ondrej/php \
    && apt-get update \
    && apt-get install -y php7.0-fpm php7.0-bz2 php7.0-gd php7.0-intl php7.0-mbstring php7.0-odbc php7.0-xml \
    && echo "deb [arch=amd64] http://apt-mo.trafficmanager.net/repos/mssql-ubuntu-xenial-release/ xenial main" > /etc/apt/sources.list.d/mssqlpreview.list \
    && apt-key adv --keyserver apt-mo.trafficmanager.net --recv-keys 417A0893 \
    && apt-get update \
    && ACCEPT_EULA=Y apt-get install -y unixodbc-dev-utf16 msodbcsql \

    #hack for msphpsql driver
    #see: https://github.com/Microsoft/msphpsql/issues/161#issuecomment-254046975
    && apt-get install -y locales \
    && echo "en_US.UTF-8 UTF-8" > /etc/locale.gen \
    && locale-gen \

    #setup php
    && sed -i "/listen = .*/c\listen = [::]:9000" /etc/php/7.0/fpm/pool.d/www.conf \
    && sed -i "/;access.log = .*/c\access.log = /proc/self/fd/2" /etc/php/7.0/fpm/pool.d/www.conf \
    && sed -i "/;clear_env = .*/c\clear_env = no" /etc/php/7.0/fpm/pool.d/www.conf \
    && sed -i "/;catch_workers_output = .*/c\catch_workers_output = yes" /etc/php/7.0/fpm/pool.d/www.conf \
    && sed -i "/pid = .*/c\;pid = /run/php/php7.0-fpm.pid" /etc/php/7.0/fpm/php-fpm.conf \
    && sed -i "/;daemonize = .*/c\daemonize = no" /etc/php/7.0/fpm/php-fpm.conf \
    && sed -i "/error_log = .*/c\error_log = /proc/self/fd/2" /etc/php/7.0/fpm/php-fpm.conf

COPY ./drivers/php_pdo_sqlsrv_7_nts.so /usr/lib/php/20151012/php_pdo_sqlsrv_7_nts.so
COPY ./drivers/php_sqlsrv_7_nts.so /usr/lib/php/20151012/php_sqlsrv_7_nts.so
COPY ./msphpsql.ini /etc/php/7.0/mods-available/msphpsql.ini

RUN ln -s /etc/php/7.0/mods-available/msphpsql.ini /etc/php/7.0/fpm/conf.d/20-msphpsql.ini \
    && ln -s /etc/php/7.0/mods-available/msphpsql.ini /etc/php/7.0/cli/conf.d/20-msphpsql.ini \
    && apt-get clean \
    && rm -rf /tmp/* /var/lib/apt/lists/* /var/tmp/*

CMD ["php-fpm7.0"]

EXPOSE 9000
