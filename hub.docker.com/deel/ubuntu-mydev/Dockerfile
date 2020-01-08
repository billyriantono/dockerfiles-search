# ubuntu-mydev
# docker build -t="deel/ubuntu-mydev:essential" .
# Author: Deel
#FROM docker.io/textlab/ubuntu-essential
FROM docker.io/deel/ubuntu-mydev:origin

MAINTAINER deel deel@d-l.top

#WORKDIR /opt


COPY ./etc/apt/sources.list /tmp/sources.list
COPY ./etc/apt/apt.conf.d/02allow-unsigned /tmp/02allow-unsigned

# Commands to update the image
RUN Utilities='dos2unix wget git vim lsof bzip2 gdbserver' \
        && set -x \ 
        && mv /etc/apt/sources.list /etc/apt/sources.list.bak \
        && mv /tmp/sources.list /etc/apt/sources.list \
        && mv /tmp/02allow-unsigned /etc/apt/apt.conf.d/02allow-unsigned \
        && apt-get update \
        && apt-get install -y software-properties-common --no-install-recommends \
        && add-apt-repository -y ppa:ubuntu-toolchain-r/test \
        && apt-get update \
        && apt-get install -y gcc-4.9 g++-4.9 gdb make cmake --no-install-recommends \
        && ln -s /usr/bin/g++-4.9 /usr/bin/g++ -f \
        && ln -s /usr/bin/gcc-4.9 /usr/bin/gcc -f \
        && ln -s /usr/bin/gcc-4.9 /usr/bin/cc -f \
        && ln -s /usr/bin/python3 /usr/bin/python -f \
        && apt-get install -y $Utilities --no-install-recommends \
        && apt-get autoclean \
        && apt-get clean \
        && apt-get autoremove \ 
        && rm -r /var/lib/apt/lists/*

# Commands when creating a new container
#CMD
