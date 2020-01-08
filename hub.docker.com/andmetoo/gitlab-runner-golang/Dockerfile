FROM golang:1.9

RUN go get github.com/mitchellh/gox
RUN go get -u github.com/golang/dep/cmd/dep
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y wget
# OpenSSL
RUN mkdir -p /usr/local/openssl/include/openssl/ && \
    ln -s /usr/include/openssl/evp.h /usr/local/openssl/include/openssl/evp.h && \
    mkdir -p /usr/local/openssl/lib/ && \
    ln -s /usr/lib/x86_64-linux-gnu/libssl.a /usr/local/openssl/lib/libssl.a && \
    ln -s /usr/lib/x86_64-linux-gnu/libssl.so /usr/local/openssl/lib/

RUN mkdir ~/.ssh/

RUN chmod 700 ~/.ssh/

# MYSQL
# /usr/bin/mysqld_safe
RUN wget -O ./RPM-GPG-KEY-mysql https://repo.mysql.com/RPM-GPG-KEY-mysql && apt-key add RPM-GPG-KEY-mysql && \
        echo "deb http://repo.mysql.com/apt/debian/ stretch mysql-5.7"  >> /etc/apt/sources.list.d/mysql.list && \
        echo "deb-src http://repo.mysql.com/apt/debian/ stretch mysql-5.7" >> /etc/apt/sources.list.d/mysql.list
RUN bash -c 'debconf-set-selections <<< "mysql-server-5.7 mysql-server/root_password password $MYSQL_ROOT_PASS"' && \
		bash -c 'debconf-set-selections <<< "mysql-server-5.7 mysql-server/root_password_again password $MYSQL_ROOT_PASS"' && \
		DEBIAN_FRONTEND=noninteractive apt-get update && \
		DEBIAN_FRONTEND=noninteractive apt-get install -qqy mysql-server

RUN rm -rf /etc/mysql/mysql.conf.d/disable_strict_mode.cnf && \
    touch /etc/mysql/mysql.conf.d/disable_strict_mode.cnf && \
    echo "[mysqld] \n sql_mode=IGNORE_SPACE,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_AUTO_CREATE_USER,NO_ENGINE_SUBSTITUTION" >> /etc/mysql/mysql.conf.d/disable_strict_mode.cnf

#Rabbitmq
RUN DEBIAN_FRONTEND=noninteractive apt-get install rabbitmq-server  -y

#Memcached
RUN DEBIAN_FRONTEND=noninteractive apt install memcached  -y

# PHP Extensions
RUN DEBIAN_FRONTEND=noninteractive apt-get update && \
    apt-get install -y -qq php-pear \
      php7.0-dev \
      php7.0-cli \
      php7.0-fpm \
      php7.0-apcu \
      php-amqp \
      php7.0-bcmath \
      php7.0-bz2 \
      php7.0-calendar \
      php7.0-common \
      php7.0-ctype \
      php7.0-curl \
      php7.0-dba \
      php7.0-dom \
      php7.0-embed \
      php7.0-enchant \
      php7.0-exif \
      php7.0-ftp \
      php7.0-gd \
      php7.0-gettext \
      php7.0-gmp \
      php7.0-iconv \
      php7.0-imagick \
      php7.0-imap \
      php7.0-intl \
      php7.0-json \
      php7.0-ldap \
      php7.0-mbstring \
      php7.0-mcrypt \
      php-memcache \
      php7.0-memcached \
      php7.0-mongodb \
      php7.0-mysqli \
      php7.0-mysqlnd \
      php7.0-odbc \
      php7.0-opcache \
#      php7.0-openssl \
      php7.0-pdo \
      php7.0-pgsql \
      php7.0-phar \
      php7.0-phpdbg \
      php7.0-posix \
      php7.0-pspell \
      php7.0-redis \
      php7.0-shmop \
      php7.0-snmp \
      php7.0-soap \
      php7.0-sockets \
      php7.0-sqlite3 \
      php7.0-sysvmsg \
      php7.0-sysvsem \
      php7.0-sysvshm \
      php7.0-tidy \
      php7.0-tokenizer \
      php7.0-wddx \
      php7.0-xdebug \
      php7.0-xml \
      php7.0-xmlreader \
      php7.0-xmlrpc \
      php7.0-xmlwriter \
      php7.0-xsl \
      php7.0-zip 

WORKDIR /go/src/app