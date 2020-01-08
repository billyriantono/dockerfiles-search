#
# Dockerfile for bbr-relay
#

FROM debian

ENV LKL_URL http://soft.91yun.org/uml/lkl/liblkl-hijack.so

WORKDIR /etc/lkl

RUN set -ex \
    && apt-get update \
    && apt-get install -y iptables haproxy wget \
    && wget --no-check-certificate "$LKL_URL" -O /etc/lkl/liblkl-hijack.so \
    && rm -rf /var/lib/apt/lists/*

COPY docker-entrypoint.sh /entrypoint.sh
COPY haproxy.cfg /etc/lkl/haproxy.cfg

ENV BIND_PORT    8080
ENV TARGET_HOST  target

EXPOSE $BIND_PORT/tcp

ENTRYPOINT ["/entrypoint.sh"]

CMD ["haproxy", "-f", "/etc/lkl/haproxy.cfg"]
