FROM ubuntu:14.04

RUN apt-get update && \
        apt-get install -y \
            curl \
            php5-fpm \
            php5-memcache \
            php5-mysql \
            php5-curl \
        && rm -rf /var/lib/apt/lists/*

RUN ln -sf /dev/stdout /var/log/php5-fpm.log

RUN sed -i -e 's/^;daemonize .*/daemonize = no/' /etc/php5/fpm/php-fpm.conf
RUN sed -i -e 's/^listen \= .*/listen = 0.0.0.0:9000/' /etc/php5/fpm/pool.d/www.conf && \
    sed -i -e 's/^pm.max_children \= .*/pm.max_children = 20/' /etc/php5/fpm/pool.d/www.conf && \
    sed -i -e 's/^;catch_workers_output = yes/catch_workers_output = yes/' /etc/php5/fpm/pool.d/www.conf

RUN curl -o /usr/local/bin/wp https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar && \
        chmod +x /usr/local/bin/wp

EXPOSE 9000

ENTRYPOINT [ "/usr/sbin/php5-fpm", "-y", "/etc/php5/fpm/php-fpm.conf" ]
