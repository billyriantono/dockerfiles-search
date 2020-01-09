ARG ALPINE_VERSION=edge

FROM alpine:$ALPINE_VERSION

ENV PACKAGER wholerencom@gmail.com
ENV PACKAGE_PRIVKEY_PUB ""
ENV PACKAGE_PRIVKEY ""

## dont chanage
ENV REPODEST /home/builder/repodest
ENV APKBUILDS /home/builder/apkbuilds

RUN apk add -U gnupg tzdata ca-certificates libressl bash file re2c 
RUN wget -qO- https://github.com/jwilder/dockerize/releases/download/v0.6.1/dockerize-alpine-linux-amd64-v0.6.1.tar.gz | tar xvz -C /usr/local/bin

RUN apk -U add alpine-sdk \
  && adduser -G abuild -g "Alpine Package Builder" -s /bin/sh -D builder \
  && echo "builder ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers \
  && rm -rf /var/cache/apk/*

COPY rootfs/_entrypoint.sh /entrypoint.sh
RUN chmod a+x /entrypoint.sh

COPY rootfs/_home_builder_.abuild_abuild.conf.tmpl /home/builder/.abuild/abuild.conf.tmpl

RUN chown -R builder /home/builder

USER builder
RUN  mkdir -p $APKBUILDS \
&& mkdir -p $REPODEST \
&& dockerize -template "/home/builder/.abuild/abuild.conf.tmpl:/home/builder/.abuild/abuild.conf"

VOLUME ["$APKBUILDS","$REPODEST"]

ENTRYPOINT ["/entrypoint.sh"]

WORKDIR $APKBUILDS

