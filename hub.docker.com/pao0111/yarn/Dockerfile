FROM alpine:edge
LABEL maintainer="pao0111@gmail.com"

RUN apk --no-cache add \
    bash git yarn

RUN mkdir -p /home/alpine && chown 1000:1000 /home/alpine
USER 1000:1000
ENV HOME /home/alpine
ENV YARN_CACHE_FOLDER /home/alpine/.cache

WORKDIR "/app"
VOLUME ["/app"]

ENTRYPOINT [ "yarn" ]
