FROM node:lts-alpine
LABEL maintainer="Fábio·Luciano"

ADD entrypoint.sh /

RUN apk add --no-cache --virtual .build-deps python2 make g++ \
    && apk add --no-cache bash \
    && npm i --unsafe-perm -g node-sass \
    && npm i -g @angular/cli \
    && apk del .build-deps \
    && chmod a+x /entrypoint.sh

VOLUME [ "/opt/source" ]
WORKDIR /opt/source

ENTRYPOINT [ "/entrypoint.sh" ]