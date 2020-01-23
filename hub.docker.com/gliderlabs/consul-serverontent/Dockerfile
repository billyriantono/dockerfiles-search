FROM node:alpine

ARG BUILD_DATE
ARG VCS_REF

LABEL maintainer                      "Guillaume LAURENT <laurent.guillaume@gmail.com>"
LABEL org.label-schema.build-date     $BUILD_DATE
LABEL org.label-schema.vcs-url        "https://github.com/iamthemitch/docker-vesync-wsproxy.git"
LABEL org.label-schema.vcs-ref        $VCS_REF
LABEL org.label-schema.name           "Etekcity WiFi Smart Plug"
LABEL org.label-schema.description    "Container to control Etekcity WiFi Smart Plug, based on vesync-wsproxy"
LABEL org.label-schema.url            "https://github.com/itsnotlupus/vesync-wsproxy"
LABEL org.label-schema.schema-version "1.0.0-rc1"

# System setup as root user
COPY --chown=node:node vesync-wsproxy /opt/vesync-wsproxy
RUN \
  # Packages and system setup
  apk --no-cache add curl drill && \
  # Clean
  rm -rf /var/cache/apk/*

# Application setup as node user
WORKDIR /opt/vesync-wsproxy
USER    node
RUN \
  # Exec rights
  chmod +x *.sh && \
  # Disable logs
  mkdir -p logs && \
  ln -s /dev/null logs/access.log && \
  ln -s /dev/null logs/server.log && \
  # Init
  npm install && \
  # Clean
  npm cache clean --force

EXPOSE  16522 17273

HEALTHCHECK --interval=5m --timeout=5s \
  CMD curl -f -X GET "http://127.0.0.1:16522/api/test" || exit 1

ENTRYPOINT [ "/opt/vesync-wsproxy/start.sh" ]
