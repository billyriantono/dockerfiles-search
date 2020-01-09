FROM suprovsky/nextcloud:17

RUN	apk add php7-imagick \
    && echo "extension=imagick.so" > /php/conf.d/imagick.ini \
    && ln /usr/lib/php7/modules/imagick.so /usr/lib/php/extensions/no-debug-non-zts-20170718/imagick.so \
    && set -x \
    && addgroup -g 82 -S www-data \
    && adduser -u 82 -D -S -G www-data www-data \
    && apk add aria2 curl php-curl \
    && mkdir /var/log/aria2c /var/local/aria2c \
    && touch /var/log/aria2c/aria2c.log \
    && touch /var/local/aria2c/aria2c.sess \
    && chown 1000:1000 -R /var/log/aria2c /var/local/aria2c \
    && chmod 770 -R /var/log/aria2c /var/local/aria2c

RUN echo "su-exec 1000 aria2c --enable-rpc --rpc-allow-origin-all -c --log=/var/log/aria2c/aria2c.log --check-certificate=false --save-session=/var/local/aria2c/aria2c.sess --save-session-interval=2 --continue=true --input-file=/var/local/aria2c/aria2c.sess --rpc-save-upload-metadata=true --force-save=true --log-level=warn &" >> /usr/local/bin/occ
