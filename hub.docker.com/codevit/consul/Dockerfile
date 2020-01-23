FROM consul:1.6.2
MAINTAINER Codev-IT <office@codev-it.at>

# copy docker scripts
COPY docker-entrypoint.sh /entrypoint
COPY docker-healthcheck.sh /healthcheck

RUN set -eux \
  # set docker scipts permission
  && chmod +x /entrypoint \
  && chmod +x /healthcheck \
  # install additional packages
  && apk add --no-cache \
    tzdata \
    mysql-client \
  && rm -rf /tmp/* /var/cache/apk/*

# docker entrypoint and commands
ENTRYPOINT ["/entrypoint"]
HEALTHCHECK CMD /healthcheck
CMD ["agent", "-client", "0.0.0.0"]

# Build-time metadata as defined at http://label-schema.org
ARG BUILD_DATE
ARG VCS_REF
ARG VERSION
LABEL org.label-schema.build-date=$BUILD_DATE \
      org.label-schema.name="consul" \
      org.label-schema.description="Docker Consul fork with more functionality." \
      org.label-schema.url="https://www.codev-it.at" \
      org.label-schema.vcs-ref=$VCS_REF \
      org.label-schema.vcs-url="https://bitbucket.org/codev-it/docker-consul.git" \
      org.label-schema.vendor="Codev-IT" \
      org.label-schema.version=$VERSION \
      org.label-schema.schema-version="1.0"