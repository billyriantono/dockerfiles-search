FROM alpine:latest
WORKDIR /tmp

RUN apk add --no-cache --virtual .build alpine-sdk curl-dev libcurl zlib-dev bzip2-dev libbz2 automake autoconf libtool libpthread-stubs && \
    apk add --no-cache libcurl libbz2
RUN git clone https://github.com/wanduow/wandio.git && \
    git clone https://github.com/CAIDA/bgpstream.git

COPY bgpstream.patch /tmp/bgpstream

RUN cd /tmp/wandio/ \
    && ./bootstrap.sh \
    && ./configure --with-http --with-zlib --with-bzip2 \
    && make \
    && make install ; \
    cd /tmp/bgpstream \
    && patch < bgpstream.patch \
    && ./autogen.sh \
    && ./configure \
    && make \
    && make install ; \
    rm -rf /tmp/wandio /tmp/bgpstream

RUN apk del .build
COPY entrypoint.sh /usr/local/bin/entrypoint.sh

ENTRYPOINT ["/usr/local/bin/entrypoint.sh","bgpreader"]
CMD ["--help"]
