# Ubuntu
FROM ubuntu:18.04

#
# UTF-8 by default
#
RUN apt-get -qq update && \
    apt-get -qqy install gnupg2 locales && \
    locale-gen en_US.UTF-8 && \
    rm -rf /var/lib/apt/lists/*

ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

# OpenJDK 8u212
ENV ZULU_VERSION=8.38.0.13

#
# Pull Zulu OpenJDK binaries from official repository:
#
RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 0xB1998361219BD9C9 && \
    echo "deb http://repos.azulsystems.com/ubuntu stable main" >> /etc/apt/sources.list.d/zulu.list && \
    apt-get -qq update && \
    apt-get -qqy install zulu-8=$ZULU_VERSION && \
rm -rf /var/lib/apt/lists/*

# Change from default Dockerfile - Install gosu
RUN set -eux; \
    apt-get update; \
    apt-get install -y gosu; \
    apt-get clean; \
    rm -rf /var/lib/apt/lists/*;\
# verify that the binary works
    gosu nobody true

# Change from default Dockerfile - end
