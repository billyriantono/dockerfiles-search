#
# Java8 Dockerfile
#
# http://github.com/buddho-io/docker-debian-java8

FROM debian:sid
MAINTAINER lance@buddho.io

ENV DEBIAN_FRONTEND noninteractive

# Install Java
RUN apt-get update && apt-get upgrade -qqy && \
    apt-get install openjdk-8-jre-headless -qqy --no-install-recommends && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

CMD ["/bin/bash"]

