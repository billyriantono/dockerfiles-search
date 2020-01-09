FROM docker:edge AS docker
FROM docker/compose:1.14.0
RUN apk --no-cache add make git
COPY --from=docker /usr/local/bin/docker /usr/local/bin/docker
ENTRYPOINT []
CMD ["docker-compose"]
