FROM gwwfps/busybox-jsruntimes:base

ENV NODE_VERSION 0.12.2

ENV PATH /node/bin:$PATH

RUN opkg-install curl libstdcpp \
  && curl -s http://nodejs.org/dist/v$NODE_VERSION/node-v$NODE_VERSION-linux-x64.tar.gz | gunzip | tar -xf - -C / \
  && opkg-cl remove curl \
  && rm -rf /var/cache/apk/* \
  && mv /node-v$NODE_VERSION-linux-x64 /node \
  && npm install -g npm \
  && npm cache clear

CMD ["node"]
