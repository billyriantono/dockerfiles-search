FROM alpine:3.5
MAINTAINER jskov@mada.dk

RUN apk update \
 && apk add --no-cache bash python libuuid iproute2 py2-dnspython \
                       lm_sensors netcat-openbsd curl iproute2 \
 && apk add --no-cache --virtual .build-deps \
                       alpine-sdk curl zlib-dev util-linux-dev \
                       libmnl-dev git autoconf automake \
		       pkgconfig \
 && git clone https://github.com/firehol/netdata.git --depth=1 \
 && cd /netdata \
 && ./netdata-installer.sh --install /opt --dont-start-it \
 && rm -rf /netdata \
 && ln -sf /dev/stdout /opt/netdata/var/log/netdata/access.log \
 && ln -sf /dev/stderr /opt/netdata/var/log/netdata/error.log \
 && apk del .build-deps


VOLUME /host

EXPOSE 19999

ENTRYPOINT ["/opt/netdata/usr/sbin/netdata"]
CMD ["-D", "-s", "/host"]
