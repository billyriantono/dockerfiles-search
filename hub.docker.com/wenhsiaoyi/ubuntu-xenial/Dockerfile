FROM ubuntu:xenial
MAINTAINER Jack Wen <http://github.com/wenhsiaoyi>

ENV LANG en_US.UTF-8
RUN locale-gen $LANG
# Common environment variables
ENV DEBIAN_FRONTEND noninteractive

RUN \

# Install dependencies
    apt-get update && apt-get install -y --no-install-recommends \
        xz-utils \
        openjdk-8-jre \
        unzip \
        curl \
        wget \
        ruby && \

# Remove cache
    apt-get clean && rm -rf /var/lib/apt/lists/* && \
    apt-get purge -y --auto-remove


CMD ["bash"]
