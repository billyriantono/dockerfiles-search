FROM ubuntu:xenial
MAINTAINER cian@cixce.com

RUN apt-get update \
 && apt-get install -y -q --no-install-recommends \
    curl \
    ca-certificates \
    build-essential \
    git \
    python \
    python3 \
    python3-pip \
 && curl -s -S -o /tmp/setup-node.sh https://deb.nodesource.com/setup_7.x \
 && chmod 755 /tmp/setup-node.sh \
 && /tmp/setup-node.sh \
 && apt-get -y -q install nodejs \
 && rm /tmp/setup-node.sh \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/* \
 && npm install -g prebuild-install \
 && npm cache clean \
 && rm -rf /tmp/*

RUN mkdir /project \
 && groupadd -g 6879 cixce \
 && useradd -u 6879 -g 6879 -ms /bin/bash cixce \
 && chown cixce.cixce /project

USER cixce
WORKDIR /project

EXPOSE 3000
CMD [“sleep”, “infinity”]
