FROM node:12.5.0-alpine
MAINTAINER abgata@abgata.jp

ENV HOME="/app" \
    LANG=C.UTF-8 \
    TZ=Asia/Tokyo \
    HOST=0.0.0.0

WORKDIR ${HOME}

RUN apk update && \
    apk upgrade && \
    apk add --no-cache git && \
    apk add curl

ENV ENTRYKIT_VERSION 0.4.0

RUN curl -LO https://github.com/progrium/entrykit/releases/download/v${ENTRYKIT_VERSION}/entrykit_${ENTRYKIT_VERSION}_Linux_x86_64.tgz && \
    tar zxvf entrykit_${ENTRYKIT_VERSION}_Linux_x86_64.tgz && \
    mv entrykit /bin/entrykit && \
    chmod +x /bin/entrykit && \
    entrykit --symlink
