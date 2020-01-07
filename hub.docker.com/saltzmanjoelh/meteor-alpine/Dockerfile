FROM mhart/alpine-node:8.15.1
ENV NODE_ENV production
RUN apk --update add python make gcc g++ git libuv bash curl tar bzip2 \
  && mkdir -p /root \
  && mkdir -p /app \
  && npm install -g npm@6.9.0 \
  && npm install -g node-gyp \
  && node-gyp install
