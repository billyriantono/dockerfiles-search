# As Jenkins slave and base image for zilliqa build

# debian:stretch based
FROM jenkins/jnlp-slave

USER root

# Zilliqa Build Dependencies
RUN apt-get update && \
    apt-get install --no-install-recommends -y \
    bash curl build-essential python-dev python-pip python-setuptools ca-certificates \
    git libboost-system-dev libboost-filesystem-dev libboost-test-dev \
    libssl-dev libleveldb-dev libjsoncpp-dev libsnappy-dev cmake libmicrohttpd-dev \
    libjsonrpccpp-dev build-essential pkg-config libevent-dev libminiupnpc-dev \
    libprotobuf-dev protobuf-compiler libcurl4-openssl-dev libboost-program-options-dev gawk && \
    rm -rf /var/lib/apt/lists/*

# ENV VERSION "17.03.1-ce"
ENV VERSION "19.03.0"
RUN curl -L -o /tmp/docker-$VERSION.tgz https://download.docker.com/linux/static/stable/x86_64/docker-$VERSION.tgz \
    && tar -xz -C /tmp -f /tmp/docker-$VERSION.tgz \
    && mv /tmp/docker/docker /usr/bin \
    && rm -rf /tmp/docker-$VERSION /tmp/docker

RUN pip install -U --no-cache-dir awscli

# the ENV user is specified in the base image
USER ${user}
