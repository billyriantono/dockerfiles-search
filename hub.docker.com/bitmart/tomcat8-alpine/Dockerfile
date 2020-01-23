FROM tomcat:8.5.27-jre8-alpine
MAINTAINER Vincent Gu <v@bitmart.com>

ENV DEP fontconfig ttf-dejavu
RUN set -ex \
    && apk add --update $DEP \
    && rm -rf /var/cache/apk/*
