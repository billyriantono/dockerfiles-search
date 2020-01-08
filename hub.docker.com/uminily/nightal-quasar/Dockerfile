FROM mhart/alpine-node:10

LABEL maintainer="Xavier HEN <uminily@gmail.com>"

RUN apk --no-cache add pkgconfig autoconf automake libtool nasm build-base zlib-dev

RUN npm install -g firebase-tools
RUN npm install -g @quasar/cli
