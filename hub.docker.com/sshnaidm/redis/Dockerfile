FROM docker.io/alpine:3.5
LABEL maintainer "sshnaidm <einarum@gmail.com>"

ENV REDIS_VERSION=3.2.5-r0

RUN apk update && \
    apk add --no-cache redis=$REDIS_VERSION bash && \
    rm -rf /root/.cache

EXPOSE 6379
CMD ["redis-server", "--protected-mode", "no"]
