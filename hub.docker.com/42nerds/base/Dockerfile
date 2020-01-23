FROM ubuntu:trusty
MAINTAINER 42nerds - Inh. Julian Kaffke <info@42nerds.com>

RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y curl wget git vim software-properties-common && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*