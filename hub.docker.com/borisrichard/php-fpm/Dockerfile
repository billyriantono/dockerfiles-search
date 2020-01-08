FROM alpine:3.5

EXPOSE 9000

ARG APK_CACHE_IP=172.17.0.1
ARG APK_CACHE_DOMAIN='dl-cdn.alpinelinux.org'

ARG BUILD_DEPS=''
ARG RUN_DEPS='php5-fpm php5-dom php5-ctype php5-curl php5-gd php5-iconv php5-intl \
              php5-json php5-opcache php5-pdo php5-pdo_mysql php5-posix php5-xml php5-soap'

RUN nc -z $APK_CACHE_IP 80 && echo $APK_CACHE_IP $APK_CACHE_DOMAIN >>/etc/hosts \
  ; apk --update add --no-cache $RUN_DEPS $BUILD_DEPS \
  && apk del $BUILD_DEPS && rm -rf /var/cache/apk/*

ADD . .

VOLUME /www

CMD ["php-fpm", "-F"]
