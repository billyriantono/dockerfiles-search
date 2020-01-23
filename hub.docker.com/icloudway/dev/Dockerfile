# This file describes basic development environment for Cloudway.

FROM debian:jessie

RUN mkdir -p /var/cache/apt/archives && touch /var/cache/apt/archives/lock

# add llvm repo
RUN apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys 6084F3CF814B57C1CF12EFD515CF4D18AF4F7421 \
	|| apt-key adv --keyserver hkp://pgp.mit.edu:80 --recv-keys 6084F3CF814B57C1CF12EFD515CF4D18AF4F7421
RUN echo deb http://llvm.org/apt/jessie/ llvm-toolchain-jessie-3.8 main > /etc/apt/sources.list.d/llvm.list

# Packaged dependencies
RUN apt-get clean && apt-get update && apt-get install -y --no-install-recommends \
    apt-utils \
    automake \
    bash-completion \
    binutils-mingw-w64 \
    bsdmainutils \
    build-essential \
    clang-3.8 \
    createrepo \
    curl \
    dpkg-sig \
    gcc-mingw-w64 \
    git \
    ssh-client \
    jq \
    libtool \
    mercurial \
    net-tools \
    pkg-config \
    python-dev \
    python-mock \
    python-pip \
    python-websocket \
    redis-server \
    tar \
    zip \
    && ln -snf /usr/bin/clang-3.8 /usr/local/bin/clang \
    && ln -snf /usr/bin/clang++-3.8 /usr/local/bin/clang++

# Configure the container for OSX cross compilation
ENV OSX_SDK MacOSX10.11.sdk
ENV OSX_CROSS_COMMIT 8aa9b71a394905e6c5f4b59e2b97b87a004658a4
RUN set -x \
    && export OSXCROSS_PATH="/osxcross" \
    && git clone https://github.com/tpoechtrager/osxcross.git $OSXCROSS_PATH \
    && (cd $OSXCROSS_PATH && git checkout -q $OSX_CROSS_COMMIT) \
    && curl -sSL https://s3.dockerproject.org/darwin/v2/${OSX_SDK}.tar.xz -o "${OSXCROSS_PATH}/tarballs/${OSX_SDK}.tar.xz" \
    && UNATTENDED=yes OSX_VERSION_MIN=10.6 ${OSXCROSS_PATH}/build.sh
ENV PATH /osxcross/target/bin:$PATH

# Install Go
# IMPORTANT: If the version of Go is updated, the Windows to Linux CI machines
#            will need updating, to avoid errors.
ENV GO_VERSION 1.12
RUN curl -fsSL "https://storage.googleapis.com/golang/go${GO_VERSION}.linux-amd64.tar.gz" \
    | tar -xzC /usr/local
ENV PATH /go/bin:/usr/local/go/bin:$PATH

#############################
# Setup testing environment #
#############################

# grab gosu for easy step-down from root
ENV GOSU_VERSION 1.7
RUN set -x \
    && apt-get update && apt-get install -y --no-install-recommends ca-certificates wget && rm -rf /var/lib/apt/lists/* \
    && wget -O /usr/local/bin/gosu "https://github.com/tianon/gosu/releases/download/$GOSU_VERSION/gosu-$(dpkg --print-architecture)" \
    && wget -O /usr/local/bin/gosu.asc "https://github.com/tianon/gosu/releases/download/$GOSU_VERSION/gosu-$(dpkg --print-architecture).asc" \
    && export GNUPGHOME="$(mktemp -d)" \
    && gpg --keyserver ha.pool.sks-keyservers.net --recv-keys B42F6819007F00F88E364FD4036A9C25BF357DD4 \
    && gpg --batch --verify /usr/local/bin/gosu.asc /usr/local/bin/gosu \
    && rm -r "$GNUPGHOME" /usr/local/bin/gosu.asc \
    && chmod +x /usr/local/bin/gosu \
    && gosu nobody true

# add our user and group first to make sure their IDs are assigned consistently,
# regardless of whatever dependencies get added
RUN groupadd -r mongodb && useradd -r -g mongodb mongodb

# pub   4096R/A15703C6 2016-01-11 [expires: 2018-01-10]
#       Key fingerprint = 0C49 F373 0359 A145 1858  5931 BC71 1F9B A157 03C6
# uid                  MongoDB 3.4 Release Signing Key <packaging@mongodb.com>
RUN apt-key adv --keyserver ha.pool.sks-keyservers.net --recv-keys 0C49F3730359A14518585931BC711F9BA15703C6

ENV MONGO_MAJOR 3.3
ENV MONGO_VERSION 3.3.10

RUN echo "deb http://repo.mongodb.org/apt/debian jessie/mongodb-org/$MONGO_MAJOR main" > /etc/apt/sources.list.d/mongodb-org.list

RUN set -x \
	&& apt-get update \
	&& apt-get install -y \
		mongodb-org-unstable=$MONGO_VERSION \
		mongodb-org-unstable-server=$MONGO_VERSION \
		mongodb-org-unstable-shell=$MONGO_VERSION \
		mongodb-org-unstable-mongos=$MONGO_VERSION \
		mongodb-org-unstable-tools=$MONGO_VERSION \
	&& rm -rf /var/lib/apt/lists/* \
	&& rm -rf /var/lib/mongodb \
	&& mv /etc/mongod.conf /etc/mongod.conf.orig

RUN apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D
RUN echo 'deb http://apt.dockerproject.org/repo debian-jessie main' > /etc/apt/sources.list.d/docker.list
RUN apt-get update && apt-get install -y docker-engine && rm -rf /var/lib/apt/lists/*
