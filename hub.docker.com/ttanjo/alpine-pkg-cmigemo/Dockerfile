FROM alpine:latest

LABEL maintainer="Tomoya Tanjo <ttanjo@gmail.com>"

ENV REPODEST /packages
ENV LOGINUSER builder

RUN apk add --no-cache alpine-sdk perl && \
    adduser -D $LOGINUSER && \
    addgroup $LOGINUSER abuild && \
    echo "$LOGINUSER ALL=(ALL) ALL" >> /etc/sudoers && \
    mkdir -p /var/cache/distfiles && \
    chgrp abuild /var/cache/distfiles && \
    chmod g+w /var/cache/distfiles && \
    curl -o /etc/apk/keys/ttanjo@gmail.com-58e06647.rsa.pub \
         https://raw.githubusercontent.com/tom-tan/alpine-pkg-nkf/master/ttanjo%40gmail.com-58e06647.rsa.pub && \
    curl -L -o nkf.apk https://github.com/tom-tan/alpine-pkg-nkf/releases/download/2.1.4-r0/nkf-2.1.4-r0.apk && \
    apk add --no-cache nkf.apk && \
    rm nkf.apk && \
    curl -SL http://ftp.gnu.org/pub/gnu/libiconv/libiconv-1.15.tar.gz | tar -xz -C /tmp/ && \
    rm /usr/bin/iconv && \
    mv /tmp/libiconv-1.15 /tmp/libiconv && \
    cd /tmp/libiconv && \
    ./configure --prefix=/usr && \
    make && make install

USER $LOGINUSER
WORKDIR /home/$LOGINUSER

RUN mkdir cmigemo
WORKDIR cmigemo
COPY APKBUILD /home/$LOGINUSER/cmigemo

COPY start.sh /
ENTRYPOINT ["/start.sh"]
