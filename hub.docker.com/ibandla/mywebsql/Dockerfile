FROM alpine:latest

# Install gnu-libconv required by php5-iconv
RUN apk add --no-cache --repository http://dl-cdn.alpinelinux.org/alpine/edge/testing gnu-libiconv
ENV LD_PRELOAD /usr/lib/preloadable_libiconv.so

# Setup apache and php
RUN apk add --no-cache apache2 php5-apache2 curl \
    php5-json php5-phar php5-openssl php5-mysql php5-curl php5-mcrypt php5-pdo_mysql php5-ctype php5-gd php5-xml php5-dom php5-iconv \
    && mkdir /run/apache2 \
    && mkdir -p /opt/utils  

EXPOSE 80
COPY . /app
CMD ["/app/start.sh"]