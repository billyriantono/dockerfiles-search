FROM alpine:3.2
RUN apk update
RUN apk add --no-progress \
    php-bcmath \
    php-bz2 \
    php-calendar \
    php-cli \
    php-common \
    php-ctype \
    php-curl \
    php-dba \
    php-dbg \
    php-doc \
    php-dom \
    php-exif \
    php-ftp \
    php-gd \
    php-gettext \
    php-gmp \
    php-iconv \
    php-imap \
    php-intl \
    php-json \
    php-ldap \
    php-mcrypt \
    php-mssql \
    php-mysql \
    php-mysqli \
    php-odbc \
    php-openssl \
    php-pdo \
    php-pdo_dblib \
    php-pdo_mysql \
    php-pdo_odbc \
    php-pdo_pgsql \
    php-pdo_sqlite \
    php-pear \
    php-pgsql \
    php-phar \
    php-posix \
    php-pspell \
    php-shmop \
    php-snmp \
    php-soap \
    php-sockets \
    php-sqlite3 \
    php-sysvmsg \
    php-sysvsem \
    php-sysvshm \
    php-wddx \
    php-xml \
    php-xmlreader \
    php-xmlrpc \
    php-xsl \
    php-zip \
    php-zlib \
    php-dev \
    make \
    gcc \
    php-fpm \
    git \
    openssl \
    openssh-client \
    bash \
    sudo \
    ca-certificates
RUN addgroup -g 1000 user
RUN adduser user -D -u 1000 -G user
RUN echo "user ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers.d/user
RUN mkdir /data
RUN chown user:user /data
VOLUME /data
ADD https://getcomposer.org/composer.phar /usr/local/bin/composer
USER user
RUN sudo chmod 755 /usr/local/bin/composer 
RUN mkdir -p /home/user/.composer
ENV PATH $PATH:/home/user/bin/
EXPOSE 8000
