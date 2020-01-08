FROM testbeds/centos:7

ENV STACK_PHP_EXTENSION_DIR=/usr/lib64/php/modules \
    STACK_PHP_CONFIG_DIR=/etc/php.d \
    STACK_APACHE_LOG=/var/log/httpd/error_log \
    STACK_APACHE_ENV_FILE=/etc/sysconfig/httpd \
    STACK_APACHE_CONFIG_DIR=/etc/httpd/conf.d

RUN yum -y install httpd php unzip wget sudo which php-pecl-memcache php-mysql php-pgsql php-pdo
RUN yum clean all -y

# apache and php
RUN printf '#!/bin/bash\nif [ -z "$(pgrep -f "httpd -k")" ]; then httpd -k start; sleep 1; fi\n' > /bin/stack_apache_start
RUN printf '#!/bin/bash\npkill -f httpd; while [ -n "$(pgrep -f "httpd -k")" ]; do sleep 1; done\n' > /bin/stack_apache_stop
RUN chmod +x /bin/stack_apache_*

# bats framework
RUN wget https://github.com/sstephenson/bats/archive/master.zip
RUN unzip master.zip
RUN bats-master/install.sh /usr/local
RUN rm -rf bats-master/ master.zip

# php-redis (build from source)
RUN rpm --rebuilddb && yum -y install php-devel gcc make
RUN wget https://github.com/phpredis/phpredis/zipball/master -O phpredis.zip
RUN unzip phpredis.zip
RUN cd phpredis-phpredis-* && phpize && ./configure && make && make install
RUN echo "extension=redis.so" > $STACK_PHP_CONFIG_DIR/redis.ini
RUN rm -rf phpredis*

# php-mongo
RUN yum -y install php-devel php-pear make gcc openssl-devel
RUN pecl install mongo
RUN echo "extension=mongo.so" > $STACK_PHP_CONFIG_DIR/mongo.ini

# php-memcached
RUN rpm --rebuilddb && yum -y install cyrus-sasl-devel zlib-devel gcc-c++ make php-devel
RUN wget https://launchpad.net/libmemcached/1.0/1.0.16/+download/libmemcached-1.0.16.tar.gz
RUN tar -xvf libmemcached-1.0.16.tar.gz
RUN cd libmemcached-1.0.16 && ./configure --disable-memcached-sasl && make && make install
RUN rm -rf libmemcached-1.0.16
RUN wget https://pecl.php.net/get/memcached-2.1.0.tgz
RUN tar xf memcached-2.1.0.tgz
RUN cd memcached-2.1.0 && phpize && ./configure && make && make install
RUN rm -rf memcached-2.1.0
RUN echo "extension=memcached.so" > $STACK_PHP_CONFIG_DIR/memcached.ini
