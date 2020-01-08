FROM ruby:2.4.2

ENV NODE_VERSION 8.9.1
COPY node-v$NODE_VERSION-linux-x64.tar.xz ./

RUN set -ex \
  && apt-get update -qq \
  && apt-get install -y build-essential libpq-dev \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/* \
  && tar -xJf "node-v$NODE_VERSION-linux-x64.tar.xz" -C /usr --strip-components=1 --no-same-owner \
  && rm "node-v$NODE_VERSION-linux-x64.tar.xz" \
  && npm install -g yarn

CMD ["node", "--version"]
