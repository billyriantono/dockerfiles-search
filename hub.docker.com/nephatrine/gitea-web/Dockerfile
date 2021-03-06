FROM nephatrine/alpine-s6:3.8
LABEL maintainer="Daniel Wolf <nephatrine@gmail.com>"

ARG GITEA_VERSION=release/v1.7

ENV GOPATH="/usr"

RUN echo "====== INSTALL PACKAGES ======" \
 && apk add \
   certbot \
   git git-lfs \
   openssh-keygen \
   openssh-server \
   sqlite \
 && apk add --virtual .build-gitea \
   build-base \
   go \
 \
 && echo "====== CONFIGURE SYSTEM ======" \
 && mkdir -p /etc/gitea \
 && usermod -p '*' -s /bin/bash guardian \
 \
 && echo "====== COMPILE GITEA ======" \
 && cd /usr/src \
 && go get -u github.com/jteeuwen/go-bindata \
 && go get -d -u code.gitea.io/gitea \
 && cd code.gitea.io/gitea \
 && git fetch && git fetch --tags \
 && git checkout "$GITEA_VERSION" \
 && PATH="$GOPATH/bin:$PATH" TAGS="bindata sqlite sqlite_unlock_notify" make generate build \
 && mv ./gitea /usr/bin/ \
 && cp ./custom/conf/app.ini.sample /etc/gitea/app.ini.sample \
 \
 && echo "====== CLEANUP ======" \
 && cd /usr/src \
 && apk del --purge .build-gitea \
 && rm -rf /tmp/* /usr/pkg/* /usr/src/* /var/cache/apk/*

EXPOSE 22/tcp 3000/tcp
COPY override /
