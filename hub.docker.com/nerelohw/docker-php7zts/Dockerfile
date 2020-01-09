FROM nerelohw/docker-php7zts-abuild:7.2.6 as php7zts-abuild

## disable gmagick b/c Segmentation Fault with php7 zts
#&& abuild.sh --mode local --repository community --package php7-gmagick

FROM nerelohw/docker-alpine:edge

ENV ALPINE_BRANCH community

COPY --from=php7zts-abuild /home/builder/repodest/$ALPINE_BRANCH /usr/src/$ALPINE_BRANCH

## install special apk
##RUN [ "$(grep -w "/usr/src/$ALPINE_BRANCH" /etc/apk/repositories)" == "" ] && sed -i "1i@local_$ALPINE_BRANCH /usr/src/$ALPINE_BRANCH" /etc/apk/repositories
##RUN apk add xxx@local_$ALPINE_BRANCH
## because local apk ,install all packages maybe reasonable
RUN apk add ghostscript-fonts imagemagick \
&& cd /usr/src/$ALPINE_BRANCH/x86_64 && apk add *.apk

##composer
COPY rootfs/_usr_local_bin/composer-installer /usr/local/bin/composer-installer
RUN chmod a+x /usr/local/bin/* \
&& cd /tmp/ \
&& composer-installer \
&& mv composer.phar /usr/local/bin/composer 

RUN sed -i 's/127.0.0.1:9000/9000/g' /etc/php7/php-fpm.d/www.conf \
&& mkdir -p /var/www/html \
&& rm -rf /usr/src/$ALPINE_BRANCH/x86_64/*

VOLUME ["/var/www/html","/tmp"]

EXPOSE 9000

CMD ["php-fpm7","-F"]
