# Builder
FROM wodby/alpine:3.10 as builder
MAINTAINER Codev-IT <office@codev-it.at>

# defaults env.
ENV PROXY_SQL_VERS=1.4.15

# build proxy-sql from source
WORKDIR /tmp
RUN set -eux \
  && apk add -t build-depends \
    git \
    cmake \
    patch \
    bzip2 \
    automake \
    zlib-dev \
    build-base \
    openssl-dev \
    libc6-compat \
    libexecinfo-dev \
  && git clone https://github.com/sysown/proxysql.git \
  && cd proxysql \
  && git checkout v$PROXY_SQL_VERS \
  && make clean \
  && make build_deps \
  && NOJEMALLOC=1 make \
  && mkdir -p /src/usr/bin \
  && mkdir -p /src/var/lib/proxysql \
  && cp -R /tmp/proxysql/src/proxysql /src/usr/bin/proxysql

# set src folder and copy build scipts
RUN set -xe \
  && mkdir -p /src/usr/local/bin \
  && cp -R /usr/local/bin/* /src/usr/local/bin/

# discovery service manger bash script
RUN set -eux \
  && git clone https://bitbucket.org/snippets/codev-it/LeaM7A/discovery-service-manager.git \
  && cd discovery-service-manager \
  && chmod +x discovery-service-manager.sh \
  && mv discovery-service-manager.sh /src/usr/bin/discovery-service

# copy local source
COPY tpl /src/etc/gotpl

# copy docker scripts
COPY docker-entrypoint.sh /src/entrypoint
COPY docker-healthcheck.sh /src/healthcheck

# copy custom bin scripts
COPY bin/docker-cron.sh /src/usr/bin/docker-cron
COPY bin/clustercheck.sh /src/usr/bin/clustercheck
COPY bin/proxysql-admin.sh /src/usr/bin/proxysql-admin

# prepare script permissions
RUN set -eux \
  && chmod +x /src/entrypoint \
  && chmod +x /src/healthcheck \
  && chmod +x /src/usr/bin/docker-cron \
  && chmod +x /src/usr/bin/clustercheck \
  && chmod +x /src/usr/bin/proxysql-admin

# Final
FROM alpine:3.10
MAINTAINER Codev-IT <office@codev-it.at>

# defaults env.
ENV MONITOR_USERNAME="monitor"\
    MONITOR_PASSWORD="monitor"

# copy build files
COPY --from=builder /src /

# install depends
RUN set -eux \
  && adduser -D -u 1000 proxy \
  && apk add --no-cache -t runtime-depends \
    jq \
    bash \
    curl \
    tzdata \
    mysql-client \
  && chown -R proxy:proxy /var/lib/proxysql

# declare volumes
VOLUME /var/lib/proxysql

# docker entrypoint and commands
ENTRYPOINT ["/entrypoint"]
HEALTHCHECK CMD /healthcheck

# ports
EXPOSE 6032 6033

# Build-time metadata as defined at http://label-schema.org
ARG BUILD_DATE
ARG VCS_REF
ARG VERSION
LABEL org.label-schema.build-date=$BUILD_DATE \
      org.label-schema.name="proxysql" \
      org.label-schema.description="Proxysql Alpine Linux with discovery service support." \
      org.label-schema.url="https://www.codev-it.at" \
      org.label-schema.vcs-ref=$VCS_REF \
      org.label-schema.vcs-url="https://bitbucket.org/codev-it/docker-databases.git" \
      org.label-schema.vendor="Codev-IT" \
      org.label-schema.version=$VERSION \
      org.label-schema.schema-version="1.0"