ARG ARCH=amd64
ARG ALPINE_VERSION=3.8
FROM $ARCH/alpine:$ALPINE_VERSION

ARG BUILD_DATE
ARG VCS_URL
ARG VCS_REF
LABEL org.label-schema.schema-version=1.0
LABEL org.label-schema.build-date=$BUILD_DATE
LABEL org.label-schema.vcs-ref=$VCS_REF
LABEL org.label-schema.vcs-url=$VCS_URL
LABEL maintainer="Andreas Treichel <gmblar+github@gmail.com>"

ARG MEMCACHED_VERSION=1.5
EXPOSE 11211
ENV MEMCACHED_MEMORY_LIMIT=64
COPY src /
RUN memcached-setup
USER memcached
HEALTHCHECK CMD memcached-healthcheck
ENTRYPOINT ["memcached-entrypoint"]
CMD ["memcached"]
