FROM progrium/busybox

MAINTAINER Marcel Harkema "http://github.com/MarcelHarkema"

RUN opkg-install git && \
    git clone git://github.com/etsy/statsd.git statsd && \
    opkg-cl remove git && \
    opkg-install curl libstdcpp && \
    rm -f /lib/libpthread.so.0 && \
    ln -s /lib/libpthread-2.18.so /lib/libpthread.so.0 && \
    curl -s http://nodejs.org/dist/v0.10.35/node-v0.10.35-linux-x64.tar.gz | gunzip | tar -xf - -C / && \
    opkg-cl remove curl

ADD ./config.js /statsd/config.js

ENV PATH node-v0.10.35-linux-x64/bin:$PATH

EXPOSE 8125/udp

CMD node /statsd/stats.js /statsd/config.js
