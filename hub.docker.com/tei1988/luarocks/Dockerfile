FROM tei1988/lua:5.2.4-alpine3.9 AS luarocks

ARG LUAROCKS_VERSION=3.0.4
ARG FILE_NAME=luarocks-${LUAROCKS_VERSION}.tar.gz
ARG FILE_URL=http://luarocks.github.io/luarocks/releases/${FILE_NAME}
ARG MD5SUM=b67be533e0e027a26e3fd2b566ac938f

USER root
RUN apk --no-cache add \
      build-base \
      lua5.2-dev \
      make
RUN wget ${FILE_URL} && \
    [ "x${MD5SUM}" = "x$(md5sum ${FILE_NAME} | awk '{print $1}')" ] && \
    tar zxvf ${FILE_NAME}
WORKDIR luarocks-${LUAROCKS_VERSION}
RUN ./configure --prefix=/usr && \
    make && \
    make install

FROM tei1988/lua:5.2.4-alpine3.8

ENV LUAROCKS_VERSION 3.0.4

USER root
RUN apk --no-cache add \
      curl \
      unzip \
      openssl
COPY --from=luarocks /usr/bin/luarocks /usr/bin/luarocks
COPY --from=luarocks /usr/bin/luarocks-admin /usr/bin/luarocks-admin
COPY --from=luarocks /etc/luarocks /etc/luarocks
COPY --from=luarocks /usr/share/lua /usr/share/lua
USER lua
