FROM alpine:3.7

RUN apk --no-cache add php7 php7-cli php7-fpm php7-mysqli php7-json php7-openssl php7-curl \
    php7-zlib php7-xml php7-phar php7-intl php7-dom php7-xmlreader php7-ctype php7-opcache \
    php7-mbstring php7-gd nginx supervisor curl curl-dev php7-xmlwriter php7-tokenizer \
    php7-session php7-zip php7-iconv php7-simplexml php7-pdo php7-redis \
    libgcc libstdc++ libx11 glib libxrender libxext libintl \
    libcrypto1.0 libssl1.0 openssh \
    ttf-dejavu ttf-droid ttf-freefont ttf-liberation ttf-ubuntu-font-family \
    && apk --no-cache --repository http://dl-3.alpinelinux.org/alpine/edge/testing/ --allow-untrusted add filebeat \
    && rm -rf /tmp/* && rm -rf /var/cache/apk/*


