FROM golang:1.13.5

LABEL name="Go Node Bedrock"
LABEL maintainer="mlussier@gmail.com"

# Env for apt-get
ENV DEBIAN_FRONTEND noninteractive


#
# gcc for cgo
#
RUN apt-get update \
  && apt-get upgrade -y \
  && apt-get install -y --no-install-recommends \
  g++ \
  wget \
  gcc \
  libc6-dev \
  libpcre++-dev \
  libsasl2-dev \
  make \
  pkg-config \
  xz-utils\
  tree \
  libssl-dev \
  libzstd-dev \
  software-properties-common \
  apt-transport-https \
  netcat \
  git \
  rpm \
  multiarch-support \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*


#
# librdkafka
#
ENV LIBRDKAFKA_VERSION 1.3.0
RUN wget https://github.com/edenhill/librdkafka/archive/v$LIBRDKAFKA_VERSION.tar.gz \
  && tar -xvf v$LIBRDKAFKA_VERSION.tar.gz  \
  && cd librdkafka-$LIBRDKAFKA_VERSION \
  && ./configure --install-deps \
  && make \
  && make install


#
# NodeJS
# Origionaly taken from https://github.com/nodejs/docker-node/blob/master/12/alpine/Dockerfile
#

ENV NPM_CONFIG_LOGLEVEL info
ENV NODE_VERSION 13.5.0

RUN set -ex \
  && for key in \
  94AE36675C464D64BAFA68DD7434390BDBE9B9C5 \
  FD3A5288F042B6850C66B31F09FE44734EB7990E \
  71DCFD284A79C3B38668286BC97EC7A07EDE3FC1 \
  DD8F2338BAE7501E3DD5AC78C273792F7D83545D \
  C4F0DFFF4E8C1A8236409D08E73BC641CC11F4C8 \
  B9AE9905FFD7803F25714661B63B535A4C206CA9 \
  77984A986EBC2AA786BC0F66B01FBB92821C587A \
  8FCCA13FEF1D0C2E91008E09770F7A9A5AE15600 \
  4ED778F539E3634C779C87C6D7062848A1AB005C \
  A48C2BEE680E841632CD4E44F07496B3EB3C1762 \
  B9E2F5981AA6E0CD28160D9FF13993A75599653C \
  ; do \
  gpg --batch --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys "$key" || \
  gpg --batch --keyserver hkp://ipv4.pool.sks-keyservers.net --recv-keys "$key" || \
  gpg --batch --keyserver hkp://pgp.mit.edu:80 --recv-keys "$key" ; \
  done

RUN ARCH= && dpkgArch="$(dpkg --print-architecture)" \
  && case "${dpkgArch##*-}" in \
  amd64) ARCH='x64';; \
  ppc64el) ARCH='ppc64le';; \
  s390x) ARCH='s390x';; \
  arm64) ARCH='arm64';; \
  armhf) ARCH='armv7l';; \
  i386) ARCH='x86';; \
  *) echo "unsupported architecture"; exit 1 ;; \
  esac \
  && curl -fsSLO --compressed "https://nodejs.org/dist/v$NODE_VERSION/node-v$NODE_VERSION-linux-$ARCH.tar.xz" \
  && curl -fsSLO --compressed "https://nodejs.org/dist/v$NODE_VERSION/SHASUMS256.txt.asc" \
  && gpg --batch --decrypt --output SHASUMS256.txt SHASUMS256.txt.asc \
  && grep " node-v$NODE_VERSION-linux-$ARCH.tar.xz\$" SHASUMS256.txt | sha256sum -c - \
  && tar -xJf "node-v$NODE_VERSION-linux-$ARCH.tar.xz" -C /usr/local --strip-components=1 --no-same-owner \
  && rm "node-v$NODE_VERSION-linux-$ARCH.tar.xz" SHASUMS256.txt.asc SHASUMS256.txt \
  && apt-get purge -y --auto-remove $buildDeps \
  && ln -s /usr/local/bin/node /usr/local/bin/nodejs

ENV NFPM_VERSION 1.1.8

RUN curl -fsSLO --compressed "https://github.com/goreleaser/nfpm/releases/download/v1.1.8/nfpm_1.1.8_Linux_x86_64.tar.gz" \
  && tar -xzvf "nfpm_1.1.8_Linux_x86_64.tar.gz" -C /usr/local/bin  --no-same-owner

#
# Install Golang deps
#
RUN go get -u github.com/golang/dep/cmd/dep \
  #
  # packr
  #
  && go get -u github.com/gobuffalo/packr/v2/packr2 \
  #
  # Swag CLI
  #
  && go get -u github.com/swaggo/swag/cmd/swag
#
# NFPM
#
#&& go get -u github.com/goreleaser/nfpm/...

#
# GolangCI Lint v1.20.0
#
RUN curl -sfL https://raw.githubusercontent.com/golangci/golangci-lint/master/install.sh| sh -s -- -b $(go env GOPATH)/bin v1.22.2 \
  #
  # Gosec 2.1.0  -  https://github.com/securego/gosec
  #
  && curl -sfL https://raw.githubusercontent.com/securego/gosec/master/install.sh | sh -s -- -b $GOPATH/bin v2.1.0


#
# Install Node deps and settings
#
RUN  /usr/local/bin/npm set progress=false \
  && /usr/local/bin/npm config set loglevel warn \
  #
  # YARN Package Manager
  #
  && npm install yarn prettier -g
