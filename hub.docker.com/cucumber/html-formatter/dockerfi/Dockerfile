FROM alpine

ADD ./certs /etc/ssl/server_certs/
COPY ./turnserver.conf /etc/
COPY ./docker-entrypoint.sh /usr/local/bin/

WORKDIR /root

RUN set -ex \
 # Build environment setup
 && apk add --no-cache --virtual .build-deps \
      autoconf \
      automake \
      build-base \
      linux-headers \
      libevent-dev \
      openssl-dev \
      sqlite \
      sqlite-dev \
      hiredis \
      hiredis-dev \
      git \
 # Build & install
 && git clone https://github.com/coturn/coturn.git \
 && cd coturn \
 && ./configure \
 && make \
 && make install \
 && apk del .build-deps \
 # Runtime dependencies setup
 && apk add --no-cache \
      $(scanelf --needed --nobanner /usr/local/bin/turn* \
      | awk '{ gsub(/,/, "\nso:", $2); print "so:" $2 }' \
      | sort -u) \
 && cd .. \
 && rm -rf ./coturn \
 && apk add curl

# SUTN/TURN PORTS
EXPOSE 3478 3479 3478/udp 3479/udp
EXPOSE 5349 5350 5349/udp 5350/udp
# CLI
EXPOSE 5766
# Relay Ports
EXPOSE 49152-65535 49152-65535/udp

ENTRYPOINT ["docker-entrypoint.sh"]
CMD ["turnserver"]
