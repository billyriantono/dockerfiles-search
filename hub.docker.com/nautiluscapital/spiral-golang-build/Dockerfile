FROM golang
MAINTAINER philip.chan@nautiluscapital.net
RUN echo "deb http://download.opensuse.org/repositories/network:/messaging:/zeromq:/release-stable/Debian_9.0/ ./" >> /etc/apt/sources.list \
    && wget https://download.opensuse.org/repositories/network:/messaging:/zeromq:/release-stable/Debian_9.0/Release.key -O- | apt-key add \
    && apt-get update \
    && apt-get install -y libzmq3-dev \
    && rm -rf /var/lib/apt/lists/*
