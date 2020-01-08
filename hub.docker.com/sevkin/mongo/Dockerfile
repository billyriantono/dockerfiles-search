FROM alpine
LABEL repository.hub="sevkin/mongo" \
      repository.url="https://github.com/sevkin/dockerfiles" \
      maintainer="Vsevolod Balashov <vsevolod@balashov.name>"
RUN apk add --update tini mongodb && rm -rf /var/cache/apk/*
VOLUME ["/data"]
WORKDIR /data
EXPOSE 27017
ENTRYPOINT ["tini", "--"]
CMD ["mongod", "--nounixsocket", "--dbpath", "./"]