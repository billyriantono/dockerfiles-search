FROM ubuntu:bionic

RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get -o Dpkg::Options::="--force-confnew" -qy install -y ruby \
    ruby-dev python-dev autoconf automake \
    git make libssl-dev libcurl4-openssl-dev libtool build-essential libapr1-dev \
    openjdk-8-jdk-headless libsasl2-dev libsvn-dev libz-dev maven sudo vim-nox \
    && apt clean && rm -rf /var/lib/apt/lists/* && gem install fpm rake

RUN useradd --home-dir /build --uid 1000 --gid 100 --shell /bin/bash build && \
    echo "build ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers

USER build

ENV PATH ${PATH}:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

ENV JAVA_HOME /usr/lib/jvm/java-8-openjdk-amd64

ADD --chown=1000 . /build

VOLUME ["/build"]

WORKDIR /build
