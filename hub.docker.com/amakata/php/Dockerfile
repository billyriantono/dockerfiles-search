FROM alpine:3.6

MAINTAINER Yoshihisa AMAKATA <amakata@gmail.com>

RUN sed -i '1s/^/https:\/\/object-storage.tyo1.conoha.io\/v1\/nc_c7e5a3f7509f4a0f8f86f0712297ff84\/alpine36\/amakata\n/'  /etc/apk/repositories
COPY amakata@gmail.com-59ad475f.rsa.pub /etc/apk/keys/amakata@gmail.com-59ad475f.rsa.pub 
RUN apk update --allow-untrusted&& \
apk add php5 php5-opcache php5-xmlrpc php5-zip php5-zlib php5-soap php5-xml php5-json php5-mcrypt php5-pdo php5-pdo_mysql php5-xsl php5-dom php5-gd php5-gettext php5-iconv php5-intl php5-apache2 php5-bcmath php5-cli php5-common php5-pear php5-xdebug php5-redis && \
apk add bash && \
rm -rf /var/cache/apk/*

RUN ln -s /usr/bin/php5 /usr/bin/php

COPY run.sh /run.sh
RUN chmod +x /run.sh

CMD "/run.sh";