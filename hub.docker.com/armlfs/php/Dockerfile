FROM alpine
WORKDIR /mnt
RUN apk -U add php7 php7-json php7-phar php7-mbstring php7-openssl php7-zlib \
  php7-dom php7-session php7-ctype php7-pdo_mysql tini
RUN ln -s /usr/bin/php7 /usr/local/bin/php
ADD https://getcomposer.org/installer /tmp/composer-setup.php
RUN php /tmp/composer-setup.php --install-dir=/usr/local/bin --filename=composer \
  && rm /tmp/composer-setup.php
EXPOSE 80
CMD exec tini php -S 0.0.0.0:80
