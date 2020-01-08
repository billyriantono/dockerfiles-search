FROM keymetrics/pm2:10-alpine
LABEL maintainer Markku Virtanen
RUN apk update && \
  apk add --no-cache git make gcc g++ python && \
  pm2 install profiler
