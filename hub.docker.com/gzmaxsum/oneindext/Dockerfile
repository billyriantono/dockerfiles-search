FROM alpine:3.10

RUN apk add --no-cache su-exec

COPY docker-nonroot-entrypoint.sh /usr/local/bin/docker-nonroot-entrypoint

ENTRYPOINT [ "docker-nonroot-entrypoint" ]
CMD [ "sh" ]
