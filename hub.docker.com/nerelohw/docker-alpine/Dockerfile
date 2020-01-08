FROM alpine:3.9

## openssl conflicts libressl
## add openssl bash file re2c graphicsmagick (image server)
RUN apk add -U gnupg tzdata ca-certificates libressl bash file re2c inotify-tools dcron htop \
               jasper-libs libpng libjpeg ghostscript tiff tiff-tools freetype graphicsmagick bind-tools

## add dockerize
RUN wget -qO- https://github.com/jwilder/dockerize/releases/download/v0.6.1/dockerize-alpine-linux-amd64-v0.6.1.tar.gz | tar xvz -C /usr/local/bin

RUN wget -O /usr/local/bin/gosu "https://github.com/tianon/gosu/releases/download/1.11/gosu-amd64" \
&& chmod a+x /usr/local/bin/gosu

## alpine repo local start
COPY keys/wholerencom@gmail.com-5b14a8f4.rsa.pub /etc/apk/keys/alpine-abuild.rsa.pub

COPY rootfs/_usr_local_bin/* /usr/local/bin/
RUN chmod a+x /usr/local/bin/*
#RUN setup-alpine-mirror -c us
