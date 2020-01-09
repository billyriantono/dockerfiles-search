FROM alpine:3.9

ARG DOCKER_TAG
ARG SOURCE_COMMIT

LABEL maintainer="Tobias Braune"
LABEL org.label-schema.version=$DOCKER_TAG \
    org.label-schema.vcs-ref=$SOURCE_COMMIT \
    org.label-schema.vcs-url="https://github.com/tbraune89/docker-tree"

RUN apk --no-cache add tree=1.8.0-r0

WORKDIR /data
VOLUME /data

ENTRYPOINT [ "tree", "/data" ]
CMD [ "-C", "-h" ]