FROM lkwg82/h2o-http2-server:v2.2.6
MAINTAINER Abe Masahiro <pen@thcomp.org>

USER root

RUN apk add -U --virtual .builders \
            curl \
            gcc \
            libc-dev \
            openssl-dev \
            perl-dev \
            make \
            wget

RUN apk add \
            dnsmasq \
            openntpd \
            perl-capture-tiny \
            perl-convert-asn1 \
            perl-crypt-openssl-bignum \
            perl-crypt-openssl-rsa \
            perl-file-copy-recursive \
            perl-file-slurp \
            perl-io-socket-ssl \
            perl-json-maybexs \
            perl-log-log4perl \
            perl-lwp-protocol-https \
            perl-module-build \
            perl-module-build-tiny \
            perl-mozilla-ca \
            perl-net-ssleay \
            perl-test-requires \
            perl-yaml-xs \
            openssh-client \
            openssl

WORKDIR /root

RUN wget -O cpm https://git.io/cpm \
 && chmod +x cpm

RUN ./cpm install -g --no-test \
                  Crypt::LE \
                  Data::Validate::IP \
                  JSON::Any \
                  Text::Xslate

RUN DDC=ddclient-3.9.0 \
 && wget -O $DDC.tar.gz "https://downloads.sourceforge.net/project/ddclient/ddclient/$DDC/$DDC.tar.gz" \
 && tar xzf $DDC.tar.gz \
 && mv $DDC/ddclient /usr/local/bin

RUN wget http://www.gcd.org/sengoku/stone/stone-2.3e.tar.gz \
 && tar xzf stone-2.3e.tar.gz \
 && cd stone-2.3d-2.3.2.7 \
 && sed -i 's/POLL/POLL -D_GNU_SOURCE/' Makefile \
 && make linux \
 && mv stone /usr/local/bin

RUN apk del .builders \
 && rm -rf /var/cache/apk/* \
           cpm \
           ddclient-* \
           stone-* \
           .perl-cpm \
           .wget-hsts

COPY ["rootfs", "/"]

VOLUME ["/ext"]
EXPOSE 22 53 67 80 123 443 8888

CMD ["/etc/rc.entry"]
