FROM tecnativa/haproxy-letsencrypt

ARG VCS_REF
ARG BUILD_DATE

LABEL maintainer="Florian Wartner <florian@mapawa.de>" \
      org.label-schema.schema-version="1.0.0" \
      org.label-schema.vendor="Florian Wartner (wartner.io)" \
      org.label-schema.build-date="$BUILD_DATE" \
      org.label-schema.vcs-ref="$VCS_REF" \
      org.label-schema.vcs-url="https://github.com/fwartner/https"

ENV STAGING=false \
    EMAIL=admin@example.com