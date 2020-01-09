FROM alpine
LABEL repository.hub="sevkin/rethinkdb" \
      repository.url="https://github.com/sevkin/dockerfiles" \
      maintainer="Vsevolod Balashov <vsevolod@balashov.name>"
RUN apk add --update tini rethinkdb && rm -rf /var/cache/apk/*
VOLUME ["/data"]
WORKDIR /data
EXPOSE 28015 29015 8080
ENTRYPOINT ["tini", "--"]
CMD ["rethinkdb", "--no-update-check", "--bind", "all"]
