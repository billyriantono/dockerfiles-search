FROM ubuntu:18.04

MAINTAINER Rasmus Nielsen

RUN apt-get clean && apt-get update
RUN apt-get install locales
RUN locale-gen en_US.UTF-8

ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8
ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update \
    && apt-get install -y nginx curl zip unzip git wget software-properties-common supervisor sqlite3 \
    gcc make autoconf libc-dev pkg-config php-xdebug \
    && add-apt-repository -y ppa:ondrej/php \
    && apt-get update \
    && apt-get install -y php7.4-dev php7.4-fpm php7.4-cli php7.4-gd php7.4-mysql \
    php7.4-pgsql php7.4-imap php-memcached php7.4-mbstring php7.4-xml php7.4-curl php7.4-soap \
    php7.4-sqlite3 php7.4-bcmath php7.4-zip php-pear zlib1g-dev mysql-client php-redis \
    && php -r "readfile('http://getcomposer.org/installer');" | php -- --install-dir=/usr/bin/ --filename=composer \
    && mkdir /run/php \
    # Clean apt-get
    && apt-get remove -y --purge software-properties-common \
    && apt-get -y autoremove \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# NGINX
RUN echo "daemon off;" >> /etc/nginx/nginx.conf \
    && ln -sf /dev/stdout /var/log/nginx/access.log \
    && ln -sf /dev/stderr /var/log/nginx/error.log \
    # PHP FPM
    && sed -i -e "s/pid =.*/pid = \/var\/run\/php7.4-fpm.pid/" /etc/php/7.4/fpm/php-fpm.conf \
    && sed -i -e "s/error_log =.*/error_log = \/proc\/self\/fd\/2/" /etc/php/7.4/fpm/php-fpm.conf \
    && sed -i -e "s/;daemonize\s*=\s*yes/daemonize = no/g" /etc/php/7.4/fpm/php-fpm.conf \
    && sed -i "s/;catch_workers_output = .*/catch_workers_output = yes/" /etc/php/7.4/fpm/pool.d/www.conf \
    # PHP
    && sed -i 's/upload_max_filesize\s=\s[0-9]*M/upload_max_filesize = 512M/' /etc/php/7.4/fpm/php.ini \
    && sed -i 's/post_max_size\s=\s[0-9]*M/post_max_size = 512M/' /etc/php/7.4/fpm/php.ini \
    && sed -i 's/memory_limit\s=\s[0-9]*M/memory_limit = 512M/' /etc/php/7.4/fpm/php.ini \
    && sed -i 's/memory_limit\s=\s[0-9]*M/memory_limit = 512M/' /etc/php/7.4/cli/php.ini

COPY default /etc/nginx/sites-available/default
COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf

EXPOSE 80

CMD ["/usr/bin/supervisord"]
