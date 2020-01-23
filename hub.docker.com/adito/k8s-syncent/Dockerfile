FROM mhart/alpine-node:6.1.0

RUN apk update && \
  apk upgrade && \
  apk add \
    mg \
    curl \
    bash \
    git \
    python rsync \
    make gcc g++ \
    bash-completion && \
  rm -rf /var/cache/apk/*

RUN npm install bower -g
