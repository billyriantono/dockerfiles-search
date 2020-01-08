# base image
FROM alpine:edge

# install node (switch to official alpine variant when released)
ENV NPM_CONFIG_LOGLEVEL 'info'
ENV NODE_VERSION '5.11.1'
RUN set -ex \
    && apk add --no-cache \
        libstdc++ \
    && apk add --no-cache --virtual .build-deps \
        binutils-gold \
        curl \
        g++ \
        gcc \
        gnupg \
        libgcc \
        linux-headers \
        make \
        paxctl \
        python \
        tar \
  && for key in \
    0034A06D9D9B0064CE8ADF6BF1747F4AD2306D93 \
    71DCFD284A79C3B38668286BC97EC7A07EDE3FC1 \
    94AE36675C464D64BAFA68DD7434390BDBE9B9C5 \
    9554F04D7259F04124DE6B476D5A82AC7E37093B \
    B9AE9905FFD7803F25714661B63B535A4C206CA9 \
    C4F0DFFF4E8C1A8236409D08E73BC641CC11F4C8 \
    DD8F2338BAE7501E3DD5AC78C273792F7D83545D \
    FD3A5288F042B6850C66B31F09FE44734EB7990E \
  ; do \
    gpg --keyserver ha.pool.sks-keyservers.net --recv-keys "$key"; \
  done \
    && curl -fSL -o "node-v$NODE_VERSION.tar.gz" \
        "https://nodejs.org/dist/v$NODE_VERSION/node-v$NODE_VERSION.tar.gz" \
    && curl -fSL -o SHASUMS256.txt.asc \
        "https://nodejs.org/dist/v$NODE_VERSION/SHASUMS256.txt.asc" \
    && gpg --batch --decrypt --output SHASUMS256.txt SHASUMS256.txt.asc \
    && grep " node-v$NODE_VERSION.tar.gz\$" SHASUMS256.txt | sha256sum -c - \
    && tar -xf "node-v$NODE_VERSION.tar.gz" \
    && cd "./node-v$NODE_VERSION" \
    && ./configure \
    && make -j$(getconf _NPROCESSORS_ONLN) \
    && make install \
    && cd .. \
    && apk del .build-deps \
    && rm -rf \
        ./node \
        node.tar.gz \
        SHASUMS256.txt \
        SHASUMS256.txt.asc

# install usefull packages
RUN set -ex \
    && apk add --no-cache \
        git \
        su-exec \
        tini
