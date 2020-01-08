FROM mhart/alpine-node:8
RUN apk update && apk add docker git
RUN apk add --no-cache --virtual .gyp \
        python make g++ gcc curl
RUN apk add fftw-dev vips-dev -q --no-progress --no-cache --repository http://nl.alpinelinux.org/alpine/edge/testing && rm -rf /var/cache/apk/*
