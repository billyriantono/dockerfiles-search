FROM alpine:latest
MAINTAINER Oscar Prieto <oprietop@uoc.edu>

RUN apk add --update --no-cache build-base \
    gcc-avr \
    avr-libc

# https://beta.docs.qmk.fm/build-compile-instructions
# <keyboard_folder>:<keymap>:<target>
ENV keyboard=niu_mini:all:all

VOLUME /qmk
WORKDIR /qmk
CMD make clean ; make ${keyboard}
