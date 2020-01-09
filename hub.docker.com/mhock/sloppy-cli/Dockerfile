FROM alpine

MAINTAINER Mojammal Hock <mojammal.hock@gmail.com>

ENV USER_HOME_DIR=/root
ENV SLOPPY_HOME="/usr/local/"
ENV PATH=${PATH}:${SLOPPY_HOME}/bin

RUN apk --update add --no-cache \
          openssl curl tar gzip bash ca-certificates git wget

RUN wget -q -O /etc/apk/keys/sgerrand.rsa.pub https://alpine-pkgs.sgerrand.com/sgerrand.rsa.pub
RUN wget https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.23-r3/glibc-2.23-r3.apk
RUN apk add glibc-2.23-r3.apk
RUN rm glibc-2.23-r3.apk

COPY sloppy-Linux-x86_64 /usr/local/bin/sloppy
RUN chmod +x /usr/local/bin/sloppy
RUN slpVer=$(sloppy version) && test $slpVer = "1.13.1" && echo "Sloppy version is -> OK" || echo "Unknown sloppy version"


