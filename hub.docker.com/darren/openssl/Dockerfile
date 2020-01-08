FROM debian:latest
WORKDIR /opt/openssl
ENTRYPOINT ["/usr/local/bin/openssl"]

ENV OPENSSL_VERSION 1.1.1-pre6

RUN apt-get update \
 && apt-get install -yq build-essential curl libz-dev \
 && curl -sSL https://www.openssl.org/source/openssl-${OPENSSL_VERSION}.tar.gz \
  | tar xfvz - --strip-components=1 -C $PWD \
 && ./config --debug \
             --prefix=/usr zlib-dynamic \
             --openssldir=/usr/local/ssl shared \
 && make \
 && make install \
 && touch /root/.rnd \
 && apt-get purge -yq build-essential curl libz-dev \
 && apt autoremove -yq \
 && rm -rf /var/lib/apt/lists/*
