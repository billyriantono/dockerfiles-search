FROM node:alpine
LABEL maintainer="Dany Laporte"

RUN apk update && \
    apk upgrade && \
    apk add --no-cache \
    bash git openssh \
    g++ gcc libgcc libstdc++ linux-headers \
    make automake python \
    alpine-sdk \
    nasm \
    autoconf \
    build-base \
    zlib \
    zlib-dev \
    libpng \
    libpng-dev\
    libwebp \
    libwebp-dev \
    libjpeg-turbo \
    libjpeg-turbo-dev && \
    npm install --quiet node-gyp -g