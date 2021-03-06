FROM golang:alpine as builder

COPY . /src
WORKDIR /src

RUN set -ex \
 && apk --no-cache add \
      bash \
      curl \
      git \
      make \
 && go get -v \
      github.com/Luzifer/named-blacklist \
      github.com/Luzifer/rootzone \
 && rootzone >named.stubs \
 && make blacklist

# ------

FROM alpine:latest

LABEL maintainer Knut Ahlers <knut@ahlers.me>

COPY build.sh /usr/local/bin/

RUN set -ex \
 && apk --no-cache add \
      bash \
      bind \
      bind-tools \
 && /usr/local/bin/build.sh

COPY --from=builder /src/named.stubs      /etc/bind/
COPY --from=builder /src/named.blacklist  /etc/bind/
COPY                named.conf            /etc/bind/
COPY                docker-entrypoint.sh  /usr/local/bin/

EXPOSE 53/udp 53

HEALTHCHECK --interval=30s --timeout=5s \
  CMD dig +short @localhost health.pdns.luzifer.io A || exit 1

ENTRYPOINT ["/usr/local/bin/docker-entrypoint.sh"]
