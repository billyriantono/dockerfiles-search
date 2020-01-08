FROM alpine

EXPOSE 8080 8443

ARG APK_CACHE_IP=172.17.0.1
ARG APK_CACHE_DOMAIN='dl-cdn.alpinelinux.org'

ARG BUILD_DEPS='libarchive-tools'
ARG RUN_DEPS='nginx openssl \
              php5-fpm php5-soap php5-dom php5-ctype php5-curl php5-gd php5-iconv \
              php5-intl php5-json php5-opcache php5-pdo php5-pdo_mysql php5-posix php5-xml'

ARG PHPVB_VERSION=5.0-5
ARG PHPVB_URL='https://sourceforge.net/projects/phpvirtualbox/files'

ENV PHPVB_HOME=/www

RUN nc -z $APK_CACHE_IP 80 && echo $APK_CACHE_IP $APK_CACHE_DOMAIN >>/etc/hosts \
  ; apk --update add --no-cache $RUN_DEPS $BUILD_DEPS \
    && mkdir -p $PHPVB_HOME && cd $PHPVB_HOME \
    && wget -O- $PHPVB_URL/phpvirtualbox-${PHPVB_VERSION}.zip | bsdtar -xf- --strip-components=1 \
    && sed -i 's|^listen =.*$|listen = /run/nginx/php5-fpm.sock|' /etc/php5/php-fpm.conf \
    && sed -i 's|^;listen.mode =.*$|listen.mode = 0666|' /etc/php5/php-fpm.conf \
    && cat /etc/php5/php-fpm.conf \
  && apk del $BUILD_DEPS && rm -rf /var/cache/apk/*

ADD . .

WORKDIR $PHPVB_HOME

VOLUME $PHPVB_HOME

CMD php-fpm; nginx -g "daemon off;"
