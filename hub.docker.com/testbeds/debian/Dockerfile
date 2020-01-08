FROM testbeds/debian:9

ENV STACK_PHP_EXTENSION_DIR=/usr/lib/php/20151012 \
    STACK_PHP_CONFIG_DIR=/etc/php/7.0/apache2/conf.d \
    STACK_APACHE_LOG=/var/log/apache2/error.log \
    STACK_APACHE_ENV_FILE=/etc/apache2/envvars \
    STACK_APACHE_CONFIG_DIR=/etc/apache2/conf-enabled

RUN apt-get update && \
    apt-get install -y curl unzip wget sudo apache2 php libapache2-mod-php php-curl php-memcache php-memcached php-mysql php-pgsql php-redis php-sqlite3 && \
    apt-get clean

# apache and php
RUN printf '#!/bin/bash\nif [ -z "$(pgrep -f "apache2 -k")" ]; then service apache2 restart; sleep 1; fi\n' > /bin/stack_apache_start
RUN printf '#!/bin/bash\nservice apache2 stop; while [ -n "$(pgrep -f "apache2 -k")" ]; do sleep 1; done\n' > /bin/stack_apache_stop
RUN chmod +x /bin/stack_apache_*
RUN a2enmod rewrite

# bats framework
RUN wget https://github.com/sstephenson/bats/archive/master.zip
RUN unzip master.zip
RUN bats-master/install.sh /usr/local
RUN rm -rf bats-master/ master.zip
