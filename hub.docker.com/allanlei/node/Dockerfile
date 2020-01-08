FROM            alpine:3.4

ENV             NPM_CONFIG_LOGLEVEL=info
ENV             NODE_VERSION=4.4.7

RUN             apk --no-cache add --virtual .node-build-deps \
                    build-base \
                    curl \
                    linux-headers \
                    binutils \
                    binutils-gold \
                    paxctl \
                    python && \
                curl -sL https://github.com/nodejs/node/archive/v$NODE_VERSION.tar.gz | tar xz -C /tmp && \
                cd /tmp/node-$NODE_VERSION && \
                ./configure --prefix=/usr/local && \
                make && \
                make install && \
                paxctl -cm /usr/local/bin/node && \
                rm -rf /tmp/* && \
                apk --no-cache add --virtual .node-run-deps \
                    libstdc++ && \
                apk del .node-build-deps

CMD             [ "node" ]
