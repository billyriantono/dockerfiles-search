FROM debian:stretch

MAINTAINER Sqreen <3
ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update \
    && apt-get install -y curl \
    && curl -s https://8dc0b36f0ea6f2f21b721765e10a7e02768cd1825b4551f4:@packagecloud.io/install/repositories/sqreen/sqreen/script.deb.sh | bash  \
    && apt-get update \
    && apt-get install -y sqreen-agent \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

EXPOSE 7773

ENTRYPOINT /usr/bin/sqreen-agent
