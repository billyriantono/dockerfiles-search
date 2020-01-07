FROM testbeds/alpine:3.7

ENV STACK_PHP_EXTENSION_DIR=/usr/lib/php7/modules \
    STACK_PHP_CONFIG_DIR=/etc/php7/conf.d \
    STACK_APACHE_LOG=/var/log/apache2/error.log \
    STACK_APACHE_ENV_FILE=/etc/apache2/envvars \
    STACK_APACHE_CONFIG_DIR=/etc/apache2/conf.d

RUN apk --update add sudo wget ca-certificates bash curl apache2 php7-apache2 php7 php7-openssl php7-memcached php7-mysqli php7-pgsql php7-pdo php7-pdo_mysql php7-pdo_pgsql php7-redis php7-curl php7-json php7-sqlite3 php7-pdo_sqlite
RUN mkdir -p /run/apache2/

# apache and php
RUN printf '#!/bin/bash\nif [ -z "$(pgrep -f "/usr/sbin/httpd")" ]; then /usr/sbin/httpd; sleep 1; fi\n' > /bin/stack_apache_start
RUN printf '#!/bin/bash\nwhile [ -n "$(pgrep -f "/usr/sbin/httpd")" ]; pkill -f /usr/sbin/httpd; do sleep 1; done\n' > /bin/stack_apache_stop
RUN chmod +x /bin/stack_apache_*
RUN sed -i 's/#\(.*mod_rewrite.so\)/\1/g' /etc/apache2/httpd.conf

# need this apache option in a docker environment
RUN printf 'HttpProtocolOptions Unsafe' >> /etc/apache2/conf.d/default.conf

# bats framework
RUN wget https://github.com/sstephenson/bats/archive/master.zip
RUN unzip master.zip
RUN bats-master/install.sh /usr/local
RUN rm -rf bats-master/ master.zip
RUN echo '$(dirname $0)/../libexec/bats "$@"' > /usr/local/bin/bats
