FROM novapo/alpine:edge
MAINTAINER Philip Graf <mail@philipgraf.de>

VOLUME /var/lib/postgresql

CMD ["/bin/s6-svscan", "/etc/s6"]

RUN apk add --no-cache \
  su-exec \
  postgresql \
  postgresql-contrib

ADD rootfs /
