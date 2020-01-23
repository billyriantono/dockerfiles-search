# http://product_installation_URL/?admin
# Default login is "admin", password is "12345".
FROM alpine:latest
MAINTAINER Andrey Arapov <andrey.arapov@nixaid.com>

# Install the dependencies
RUN apk update && \
    apk add tzdata wget unzip gnupg1 nginx php7-fpm \
            php7-curl php7-json php7-dom php7-zlib php7-iconv php7-openssl \
            php7-pdo_sqlite php7-pdo_mysql php7-pdo_pgsql

# Create the application user so that PHP-FPM can run
ENV USER rainloop
ENV UID 7008
ENV HOME /home/$USER
ENV DATA /opt/rainloop
RUN adduser -D -u $UID -h $HOME -s /bin/true $USER && \
    mkdir -p $DATA && \
    touch /var/log/php-fpm.log && \
    chown -Rh $USER:$USER $DATA /var/log/php-fpm.log

# Prepare the environment so that nginx can run as non-root
RUN mkdir -p /var/log/rainloop /var/lib/nginx/tmp && \
    ( cd /var/lib/nginx/tmp && \
      for i in client_body proxy fastcgi uwsgi scgi; do mkdir $i; done ) && \
    ( cd /var/log/nginx && \
      touch error.log access.log ) && \
    touch /var/run/nginx.pid && \
    chown -Rh nginx:nginx /var/log/nginx /var/lib/nginx /var/run/nginx.pid /var/log/rainloop /var/tmp/nginx

# Obtain the latest version of the RainLoop Webmail Community edition,
# verify its integrity using GnuPG and then decompress it
USER $USER
ENV RLFILE rainloop-community-latest.zip
ENV RLFILESIG rainloop-community-latest.zip.asc
ENV FINGERPRINT "3B797ECE694F3B7B70F311A4ED7C49D987DA4591"
WORKDIR $DATA
RUN wget -O $RLFILE http://repository.rainloop.net/v2/webmail/$RLFILE && \
    wget -O $RLFILESIG http://repository.rainloop.net/v2/webmail/$RLFILESIG && \
    export GNUPGHOME="$(mktemp -d)" && \
    gpg --keyserver ha.pool.sks-keyservers.net --recv-keys "$FINGERPRINT" && \
    gpg --batch --verify $RLFILESIG $RLFILE && \
    unzip $RLFILE && \
    rm -rf "$GNUPGHOME" $RLFILE

# Copy the nginx configs and then launch the PHP-FPM and Nginx
USER root
COPY rainloop.conf /etc/nginx/conf.d/rainloop.conf
COPY nginx.conf /etc/nginx/nginx.conf
COPY php-fpm.conf /etc/php7/php-fpm.conf

# Set correct permissions and ownership
RUN find $DATA -xdev -type d -exec chmod u=rwx,g=rx,o= '{}' \; && \
    find $DATA -xdev -type f -exec chmod u=rw,g=r,o= '{}' \; && \
    chown -Rh $USER:nginx /opt/rainloop /var/lib/nginx/tmp && \
    chgrp -Rh nginx /etc/nginx

CMD /bin/sh -c "su -s /bin/sh $USER -c php-fpm7 && \
                su -s /bin/sh nginx -c nginx"

VOLUME [ "/opt/rainloop/data", "/var/log/rainloop" ]
EXPOSE 80/tcp
