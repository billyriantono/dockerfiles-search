FROM ubuntu:14.04

MAINTAINER Emil Haugbergsmyr <emil@raeven.net>

LABEL ubuntu.version="14.04" confd.version="0.9.0"

RUN apt-get update && apt-get upgrade -y && apt-get install -y curl

# Install confd
RUN curl -qL https://github.com/kelseyhightower/confd/releases/download/v0.9.0/confd-0.9.0-linux-amd64 -o /confd && chmod +x /confd && mkdir -p /etc/confd/conf.d && mkdir -p /etc/confd/templates
