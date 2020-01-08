FROM kmelkez/php-base:latest
MAINTAINER Matthieu Keromen <sharoomsorg@gmail.com>
ENV REFRESHED_AT 2015-06-01

RUN apt-get install -y \
    php-pear && \
    pecl install xdebug && \
    rm -rf /var/lib/apt/lists/*

RUN wget --no-check-certificate https://phar.phpunit.de/phpunit.phar && \
    chmod +x phpunit.phar && \
    mv phpunit.phar /usr/local/bin/phpunit

ENTRYPOINT ["/bin/bash"]
