FROM exira/base:latest

MAINTAINER exira.com <info@exira.com>

ENV DOKUWIKI_VERSION=2015-08-10a \
    DOKUWIKI_MD5=a4b8ae00ce94e42d4ef52dd8f4ad30fe

RUN apk update && \
    apk upgrade && \
    apk add --update --no-cache wget && \

    # download unpack dokuwiki
    mkdir /tmp/dokuwiki/ && \
    cd /tmp/dokuwiki/ && \

    wget http://download.dokuwiki.org/src/dokuwiki/dokuwiki-${DOKUWIKI_VERSION}.tgz -O /tmp/dokuwiki.tgz && \
    if [ "${DOKUWIKI_MD5}" != "$(md5sum /tmp/dokuwiki.tgz | awk '{print($1)}')" ];then echo "Wrong md5sum of downloaded file!"; exit 1; fi && \

    mkdir -p /var/www/public_html/ && \
    tar xvfz /tmp/dokuwiki.tgz -C /var/www/public_html && \
    mv /var/www/public_html/dokuwiki-${DOKUWIKI_VERSION}/* /var/www/public_html/ && \
    rm -rf /var/www/public_html/dokuwiki-${DOKUWIKI_VERSION} && \
    rm -f /tmp/dokuwiki.tgz && \

    # add www-data user
    mkdir -p /home/www-data && \
    addgroup -g 433 -S www-data && \
    adduser -u 431 -S -D -G www-data -h /home/www-data -s /sbin/nologin www-data && \
    chown -R www-data:www-data /home/www-data && \

    # cleanup
    apk del wget && \
    rm -rf /var/cache/apk/*

RUN chown -R www-data:www-data /var/www

WORKDIR /var/www/

VOLUME /var/www/
