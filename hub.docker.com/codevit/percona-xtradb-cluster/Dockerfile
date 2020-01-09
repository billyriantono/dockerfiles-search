# Builder
FROM alpine:3.10 as builder
MAINTAINER Codev-IT <office@codev-it.at>

# build depends.
WORKDIR /tmp
RUN set -eux \
  && apk add -t build-depends \
    git \
  && mkdir -p /src/usr/bin

# discovery service manger bash script
RUN set -eux \
  && git clone https://bitbucket.org/snippets/codev-it/LeaM7A/discovery-service-manager.git \
  && cd discovery-service-manager \
  && chmod +x discovery-service-manager.sh \
  && mv discovery-service-manager.sh /src/usr/bin/discovery-service

# copy docker scripts
COPY docker-entrypoint.sh /src/entrypoint.sh
COPY docker-healthcheck.sh /src/healthcheck

# copy custom bin scripts
COPY bin/docker-cron.sh /src/usr/bin/docker-cron

# prepare script permissions
RUN set -eux \
  && chmod +x /src/entrypoint.sh \
  && chmod +x /src/healthcheck \
  && chmod +x /src/usr/bin/docker-cron

# Final
FROM percona/percona-xtradb-cluster:5.7
MAINTAINER Codev-IT <office@codev-it.at>

# set user to build
USER root

# copy build files
COPY --from=builder /src /

# set workung user
USER 1001

# docker entrypoint and commands
HEALTHCHECK --start-period=45s CMD /healthcheck

# Build-time metadata as defined at http://label-schema.org
ARG BUILD_DATE
ARG VCS_REF
ARG VERSION
LABEL org.label-schema.build-date=$BUILD_DATE \
      org.label-schema.name="percona-xtradb-cluster" \
      org.label-schema.description="Docker Percona-Xtradb-Cluster fork with more functionality." \
      org.label-schema.url="https://www.codev-it.at" \
      org.label-schema.vcs-ref=$VCS_REF \
      org.label-schema.vcs-url="https://bitbucket.org/codev-it/docker-databases.git" \
      org.label-schema.vendor="Codev-IT" \
      org.label-schema.version=$VERSION \
      org.label-schema.schema-version="1.0"