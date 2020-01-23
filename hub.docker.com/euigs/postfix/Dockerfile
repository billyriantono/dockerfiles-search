FROM alpine:edge

ARG BUILD_DATE=0
ARG VCS_REF=0
ARG VERSION=3.4.1

LABEL maintainer="Ernesto Pérez <ernesto.perez@euigs.com>" \
      org.label-schema.build-date=$BUILD_DATE \
      org.label-schema.name="Postfix" \
      org.label-schema.description="Postfix docker images based on Alpine Linux" \
      org.label-schema.url="https://cloud.docker.com/u/euigs/repository/docker/euigs/postfix" \
      org.label-schema.vcs-ref=$VCS_REF \
      org.label-schema.vcs-url="https://github.com/aeperez/docker-postfix" \
      org.label-schema.vendor="EUIGS" \
      org.label-schema.version=$VERSION \
      org.label-schema.schema-version="1.0"

RUN set -ex && \
    apk add --update --no-cache \
    postfix \
    ca-certificates

COPY root /

EXPOSE 25/tcp

ENTRYPOINT ["/usr/local/sbin/entry-point.sh"]
CMD ["/usr/sbin/postfix", "-v", "start-fg"]
