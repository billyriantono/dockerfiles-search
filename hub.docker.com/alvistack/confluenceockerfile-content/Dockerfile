FROM php:apache
MAINTAINER Alisson Martineli <martineli.alisson@gmail.com>

RUN /usr/sbin/a2enmod rewrite

COPY 000-phalcon.conf /etc/apache2/sites-available/
RUN /usr/sbin/a2ensite 000-phalcon

RUN /usr/bin/apt-get update && apt-get install -y git \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /tmp
RUN git clone --depth=1 https://github.com/phalcon/zephir.git \
    && find zephir -type f -print0 | xargs -0 sed -i 's/sudo //g' \
    && cd zephir \
    && ./install -c

WORKDIR /tmp
RUN git clone --branch 2.1.x --depth=1 https://github.com/phalcon/cphalcon.git \
    && cd cphalcon \
    && zephir fullclean \
    && zephir build --backend=ZendEngine3 \
    && echo "extension=phalcon.so" >> /usr/local/etc/php/conf.d/30-phalcon.ini

EXPOSE 80

CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]
