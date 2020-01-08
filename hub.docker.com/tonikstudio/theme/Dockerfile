FROM tonikstudio/base:latest

RUN echo "@edge http://nl.alpinelinux.org/alpine/edge/main" >> /etc/apk/repositories \
    && apk add --update \
        libuv@edge \
        nodejs@edge \
        nodejs-npm@edge \
    && rm -rf /var/cache/apk/*

RUN apk add --update \
        php7 \
        php7-zip \
        php7-json \
        php7-phar \
        php7-ctype \
        php7-openssl \
        php7-mbstring \
        php7-xmlwriter \
        php7-simplexml \
        php7-tokenizer \
    && ln -nfs /usr/bin/php7 /usr/bin/php \
    && ln -nfs /etc/php7 /etc/php \
    && rm -rf /var/cache/apk/*

RUN apk add --update \
        curl \
        openssh \
        openssh-client \
        ca-certificates \
    && rm -rf /var/cache/apk/*

COPY --from=composer:1.7 /usr/bin/composer /usr/bin/composer

CMD ["npm", "php", "composer"]
