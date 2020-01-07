FROM miko2u/alpine

RUN cd /tmp \
 && apk add nodejs \
    --update \
    --repository http://dl-cdn.alpinelinux.org/alpine/edge/main/ \
 && rm -rf /var/cache/apk/* \
 && npm -g install npm \
 && find /usr/lib/node_modules/npm -name test -o -name .bin -type d | xargs rm -rf \
 && rm -rf /root/.npm \
    /usr/lib/node_modules/npm/man /usr/lib/node_modules/npm/doc /usr/lib/node_modules/npm/html
