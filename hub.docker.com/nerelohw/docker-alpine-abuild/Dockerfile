ARG ALPINE_VERSION=3.8

FROM alpine:$ALPINE_VERSION

ENV ALPINE_VERSION edge
ENV PACKAGER wholerencom@gmail.com

ENV ALPINE_USER builder
ENV PACKAGER_PRIVKEY /home/$ALPINE_USER/.abuild/alpine-abuild.rsa
ENV PACKAGER_PRIVKEY_PUB /etc/apk/keys/alpine-abuild.rsa.pub
ENV REPODEST /home/builder/repodest
ENV APKBUILDS /home/builder/apkbuilds

RUN apk add -U gnupg tzdata ca-certificates libressl bash file re2c git

RUN apk -U add alpine-sdk \
  && adduser -G abuild -g "Alpine Package Builder" -s /bin/sh -D $ALPINE_USER \
  && echo "$ALPINE_USER ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers \
  && mkdir -p /etc/apk/keys \
  && rm -rf /var/cache/apk/*

COPY rootfs/abuild.sh /usr/local/bin/abuild.sh
COPY keys/wholerencom@gmail.com-5b14a8f4.rsa $PACKAGER_PRIVKEY
COPY keys/wholerencom@gmail.com-5b14a8f4.rsa.pub $PACKAGER_PRIVKEY_PUB
RUN chmod a+x /usr/local/bin/abuild.sh

USER $ALPINE_USER

COPY rootfs/abuild.conf  $HOME/.abuild/abuild.conf

RUN  mkdir -p $APKBUILDS $REPODEST 

VOLUME ["$APKBUILDS"]

WORKDIR $APKBUILDS

