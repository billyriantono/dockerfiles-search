FROM mhart/alpine-node:8
ENV ROOT /usr/src/

VOLUME /usr/src/

RUN apk update && apk add --no-cache \
    git \
    # Prerequisites for pngquant-bin
    build-base \
    libpng-dev \
    lcms2-dev \
    pkgconfig \
    autoconf \
    automake \
    libtool \
    nasm \
    bash
RUN npm install -g webpack

WORKDIR /usr/src

ENTRYPOINT yarn && npm run-script build