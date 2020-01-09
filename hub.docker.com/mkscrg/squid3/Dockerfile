FROM alpine:3.5

RUN set -e; \
  apk add --update build-base perl; \
  rm -rf /var/cache/apk /etc/apk/cache

RUN set -e; \
  cd ~; \
  wget http://www.squid-cache.org/Versions/v3/3.5/squid-3.5.25.tar.gz; \
  tar -vxf squid-3.5.25.tar.gz; \
  cd squid-3.5.25; \
  ./configure --prefix=/usr/local/squid; \
  make all; \
  make install; \
  cd ~; \
  rm -r squid-3.5.25*

RUN adduser -D proxy

USER proxy

CMD /usr/local/squid/sbin/squid -N -f /var/squid/squid.conf
