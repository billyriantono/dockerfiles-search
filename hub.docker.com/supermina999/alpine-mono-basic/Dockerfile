FROM frolvlad/alpine-mono

RUN apk add --no-cache --virtual=.build-dependencies wget ca-certificates tar xz && \
    wget "https://archive.archlinux.org/packages/m/mono-basic/mono-basic-4.6-2-x86_64.pkg.tar.xz" -O "/tmp/mono-basic.pkg.tar.xz" && \
    tar -xJf "/tmp/mono-basic.pkg.tar.xz" && \
    cert-sync /etc/ssl/certs/ca-certificates.crt && \
    apk del .build-dependencies && \
    rm /tmp/*
