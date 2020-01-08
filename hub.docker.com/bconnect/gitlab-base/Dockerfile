FROM mhart/alpine-node:10

RUN apk add --update python make g++ libpng-dev autoconf zlib zlib-dev automake libtool nasm
RUN apk --no-cache add curl git subversion openssh openssl mercurial tini bash zlib-dev bash coreutils

RUN echo "===> Installing sudo to emulate normal OS behavior..."  && \
    apk --update add sudo                                         && \
    \
    \
    echo "===> Adding Python runtime..."  && \
    apk --update add python py-pip openssl ca-certificates    && \
    apk --update add --virtual build-dependencies \
                python-dev libffi-dev openssl-dev build-base  && \
    pip install --upgrade pip cffi                            && \
    \
    \
    echo "===> Installing Ansible..."  && \
    pip install ansible                && \
    \
    \
    echo "===> Installing handy tools (not absolutely required)..."  && \
    pip install --upgrade pywinrm                  && \
    apk --update add sshpass openssh-client rsync  && \
    \
    \
    echo "===> Removing package list..."  && \
    apk del build-dependencies            && \
    rm -rf /var/cache/apk/*               && \
    \
    \
    echo "===> Adding hosts for convenience..."  && \
    mkdir -p /etc/ansible                        && \
    echo 'localhost' > /etc/ansible/hosts

ADD https://php.codecasts.rocks/php-alpine.rsa.pub /etc/apk/keys/php-alpine.rsa.pub
RUN apk --update add ca-certificates


RUN apk add --update curl
RUN apk add --update php7
RUN apk add --update php7-cli
RUN apk add --update php7-curl
RUN apk add --update php7-openssl
RUN apk add --update php7-json
RUN apk add --update php7-phar
RUN apk add --update php7-dom
RUN apk add --update php7-json
RUN apk add --update php7-xml
RUN apk add --update php7-zip
RUN apk add --update php7-iconv
RUN apk add --update php7-mbstring
RUN apk add --update php7-curl
RUN apk add --update php7-zlib
RUN apk add --update php7-ctype
RUN apk add --update php7-simplexml
RUN apk add --update php7-gd

RUN apk add --update gifsicle
RUN apk add --update optipng

RUN apk add --update unzip
RUN apk add --update patch

RUN apk --update add autoconf automake build-base libtool nasm 

ENV COMPOSER_ALLOW_SUPERUSER 1
ENV COMPOSER_HOME /composer
ENV COMPOSER_VERSION 1.6.5

RUN apk add --update build-base autoconf automake file libtool nasm libpng-dev

RUN set -x;\
	npm install mozjpeg; \
	./node_modules/mozjpeg/vendor/cjpeg -version; \
	ldd ./node_modules/mozjpeg/vendor/cjpeg

RUN set -x;\
	npm install cwebp-bin

RUN curl -s -f -L -o /tmp/installer.php https://raw.githubusercontent.com/composer/getcomposer.org/b107d959a5924af895807021fcef4ffec5a76aa9/web/installer \
 && php -r " \
    \$signature = '544e09ee996cdf60ece3804abc52599c22b1f40f4323403c44d44fdfdd586475ca9813a858088ffbc1f233e9b180f061'; \
    \$hash = hash('SHA384', file_get_contents('/tmp/installer.php')); \
    if (!hash_equals(\$signature, \$hash)) { \
        unlink('/tmp/installer.php'); \
        echo 'Integrity check failed, installer is either corrupt or worse.' . PHP_EOL; \
        exit(1); \
    }" \
 && php /tmp/installer.php --no-ansi --install-dir=/usr/bin --filename=composer --version=${COMPOSER_VERSION} \
 && composer --ansi --version --no-interaction \
&& rm -rf /tmp/* /tmp/.htaccess

RUN apk add --no-cache --repository http://dl-3.alpinelinux.org/alpine/edge/testing gnu-libiconv
ENV LD_PRELOAD /usr/lib/preloadable_libiconv.so php

ENV PATH /composer/vendor/bin:$PATH
ENV COMPOSER_ALLOW_SUPERUSER 1
ENV COMPOSER_EXIT_ON_PATCH_FAILURE 1

RUN composer global require hirak/prestissimo
