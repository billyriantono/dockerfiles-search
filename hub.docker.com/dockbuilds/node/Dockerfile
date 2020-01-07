FROM debian:jessie

ENV NODE_VERSION 0.11.13

RUN apt-get update && apt-get install -y \
  python \
  g++ \
  ca-certificates \
  make \
  curl \
  && rm -rf /var/lib/apt/lists/*

RUN curl http://nodejs.org/dist/v$NODE_VERSION/node-v$NODE_VERSION-linux-x64.tar.gz | \
  tar -C /usr/local --strip-components=1 -xvz \
  && apt-get purge -y curl \
  && apt-get autoremove -y

CMD ["node"]