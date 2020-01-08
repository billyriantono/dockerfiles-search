# Dockerfile for cpuminer mining veltor
# https://bitcointalk.org/index.php?topic=1583655.0
# usage: docker run marsmensch/cpuminer-veltor -a sib -t 8 -s 6 -o stratum+tcp://veltor.suprnova.cc:8897 -u username.worker -p x -q
#
FROM		ubuntu:16.04
MAINTAINER Florian Maier <contact@marsmenschen.com>

ENV GIT_URL git://github.com/marsmensch/cpuminer-veltor.git
ENV REFRESHED_AT 2016-08-22

# install dependencies
RUN apt-get autoclean && apt-get autoremove && apt-get update && \
    apt-get -qqy install --no-install-recommends build-essential \
    automake libcurl4-openssl-dev libssl-dev \
    make autoconf automake libtool git apt-utils pkg-config \
    libcurl3-dev libudev-dev && \
    rm -rf /var/lib/apt/lists/*

# create code directory
RUN mkdir -p /opt/code/; cd /opt/code; git clone ${GIT_URL} cpuminer && \
    cd cpuminer && ./autogen.sh && \
    ./configure CFLAGS="-march=native" LIBS="-lcurl -lssl -lcrypto -lz" && \
    make && make install && rm -rf /opt/code/

# no parameters display help
ENTRYPOINT ["/usr/local/bin/cpuminer"]
CMD ["--help"]
