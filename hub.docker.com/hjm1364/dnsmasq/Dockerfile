FROM alpine:latest


RUN apk add --update --no-cache --virtual .build-deps \
      build-base \
      libcap-dev \
      git

RUN mkdir /tmp/repo \
    && cd /tmp/repo \
    && git clone http://thekelleys.org.uk/git/dnsmasq.git \
    && cd dnsmasq \
    && git checkout v2.80 \
    && make install

RUN apk del .build-deps \
    && rm -rf /tmp/repo

RUN mkdir /conf \
    && touch dnsmasq.conf \
    && echo "user=root" > /conf/dnsmasq.conf

ENTRYPOINT ["dnsmasq", "-k", "--conf-file=/conf/dnsmasq.conf"]
