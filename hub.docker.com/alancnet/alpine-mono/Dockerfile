FROM alancnet/alpine-glibc:3.4

RUN apk add --update curl wget ca-certificates tar xz autoconf libtool pkgconf make git automake && \
      cd /tmp && \
      wget "http://mirror.hactar.xyz/extra/os/x86_64/mono-5.0.0.100-1-x86_64.pkg.tar.xz" -O mono.pkg.tar.xz && \
      cd / && \
      tar xJf /tmp/mono.pkg.tar.xz && \
      mozroots --url http://anduin.linuxfromscratch.org/BLFS/other/certdata.txt --import --ask-remove && \
      apk del tar xz autoconf libtool pkgconf automake && \
      update-ca-certificates && \
      wget https://curl.haxx.se/ca/cacert.pem && \
      cert-sync cacert.pem && \
      rm -rf /tmp/src /cacert.pem && \
      rm -rf /tmp/* /var/cache/apk/*
