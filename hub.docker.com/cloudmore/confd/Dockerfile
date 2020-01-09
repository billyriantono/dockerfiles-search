FROM alpine

ARG APK_CACHE_IP=172.17.0.1
ARG APK_CACHE_DOMAIN='dl-cdn.alpinelinux.org'

ARG RUN_DEPS=''
ARG BUILD_DEPS='go git musl-dev'

ARG GOPATH=/tmp
ARG GOBIN=/usr/sbin
ARG GOPKG=/usr/lib/go/pkg

RUN nc -z $APK_CACHE_IP 80 && echo $APK_CACHE_IP dl-cdn.alpinelinux.org >>/etc/hosts \
  ; apk --update add --no-cache $RUN_DEPS $BUILD_DEPS \
    && go get -u github.com/kelseyhightower/confd  \
  && apk del $BUILD_DEPS && rm -rf /var/cache/apk/* $GOPATH $GOPKG

WORKDIR /etc/confd

CMD ["confd"]
