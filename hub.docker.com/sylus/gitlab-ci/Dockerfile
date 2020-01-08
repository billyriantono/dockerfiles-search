FROM docker:18.09
MAINTAINER William Hearn <sylus1984@gmail.com>, Zachary Seguin <zachary@zacharyseguin.ca>

# Custom additions for test runner.
RUN apk --update add \
    bash \
    curl \
    ca-certificates \
    git \
    make \
    openssh-client \
    patch \
    tar \
    openssl

# Docker Compose with glibc bypass.
RUN curl --silent -o /etc/apk/keys/sgerrand.rsa.pub https://alpine-pkgs.sgerrand.com/sgerrand.rsa.pub && \
    curl --silent -Lo glibc.apk https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.29-r0/glibc-2.29-r0.apk && \
    apk add glibc.apk && \
    rm /etc/apk/keys/sgerrand.rsa.pub glibc.apk && \
    ln -s /lib/libz.so.1 /usr/glibc-compat/lib/ && \
    ln -s /lib/libc.musl-x86_64.so.1 /usr/glibc-compat/lib && \
    ln -s /usr/lib/libgcc_s.so.1 /usr/glibc-compat/lib

# Install PHP.
RUN apk --no-cache --update add \
    openssl-dev \
    libwebp \
    php7 \
    php7-xml \
    php7-xsl \
    php7-pdo_mysql \
    php7-mcrypt \
    php7-curl \
    php7-json \
    php7-fpm \
    php7-phar \
    php7-openssl \
    php7-mysqli \
    php7-ctype \
    php7-opcache \
    php7-mbstring \
    php7-simplexml \
    php7-tokenizer \
    php7-xmlwriter \
    php7-zip \
    php7-zlib \
    php7-gd \
    php7-session

# Correct paths.
RUN ln -s /etc/php7 /etc/php && \
    ln -s /usr/sbin/php-fpm7 /usr/bin/php-fpm && \
    ln -s /usr/lib/php7 /usr/lib/php

# Install Composer.
RUN curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer

# Install Docker Compose.
RUN curl -Lo docker-compose https://github.com/docker/compose/releases/download/1.18.0/docker-compose-Linux-x86_64 && \
    chmod +x docker-compose && \
    mv docker-compose /usr/local/bin

COPY docker-entrypoint.sh /usr/local/bin/

ENTRYPOINT ["docker-entrypoint.sh"]
CMD ["sh"]
