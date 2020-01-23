FROM ubuntu:trusty
MAINTAINER cian@cixce.com

RUN apt-get update \
 && apt-get install -y -q --no-install-recommends \
    curl \
    ca-certificates \
    build-essential \
 && curl -s -S -o /tmp/setup-node.sh https://deb.nodesource.com/setup_8.x \
 && chmod 755 /tmp/setup-node.sh \
 && /tmp/setup-node.sh \
 && apt-get -y -q install nodejs \
 && rm /tmp/setup-node.sh \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/* \
 && npm install -g prebuild-install

RUN mkdir /project
WORKDIR /project

EXPOSE 3000
CMD ["/bin/bash"]
