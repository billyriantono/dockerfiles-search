FROM alpine:latest

ENV VERSION=v0.12.7

RUN apk add --update wget build-base linux-headers python ca-certificates paxctl

RUN wget https://nodejs.org/dist/latest/node-${VERSION}.tar.gz && \
  tar xzf node-${VERSION}.tar.gz && \
  cd node-${VERSION} && \
  ./configure --prefix=/usr && \
  make -j4 && make install && \
  paxctl -cm /usr/bin/node && \
  npm install -g npm && \
  apk del wget paxctl && \
  rm -rf /node-${VERSION}.tar.gz /node-${VERSION} /usr/share/man /tmp/* /root/.npm /root/.node-gyp \
    /usr/lib/node_modules/npm/man /usr/lib/node_modules/npm/doc /usr/lib/node_modules/npm/html

CMD [ "node" ]
