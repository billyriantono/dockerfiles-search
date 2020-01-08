#
# Java7 Dockerfile
#
# http://github.com/buddho-io/docker-debian-java7

FROM debian:sid
MAINTAINER lance@buddho.io

ENV DEBIAN_FRONTEND noninteractive

# Install HAProxy
RUN apt-get update && apt-get upgrade -qqy && \
    apt-get install openjdk-7-jre-headless -qqy --no-install-recommends && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

CMD ["/bin/bash"]
