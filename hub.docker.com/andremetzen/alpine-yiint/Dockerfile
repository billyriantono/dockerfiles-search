FROM alpine:3.8

RUN apk update && apk upgrade && \
    apk add --no-cache \
        apache2 \
        php7 \
        php7-apache2 \
        php7-curl \
        php7-ctype \
        php7-dom \
        php7-gd \
        php7-json \
        php7-mbstring \
        php7-openssl \
        php7-session \
        php7-simplexml \
        php7-xml \
        php7-zip

COPY httpd.conf /etc/apache2

COPY httpd-foreground.sh /usr/local/bin/

RUN chmod 777 /usr/local/bin/httpd-foreground.sh && \
    mkdir -p /run/apache2

EXPOSE 80

CMD ["httpd-foreground.sh"]
