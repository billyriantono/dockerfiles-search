FROM jenkins/jenkins:lts-alpine
ARG VERSION
ARG VCS_REF
ARG BUILD_DATE
ARG ARG_ATTEMPTS
ARG ARG_TIMEOUT
ARG ARG_SUCCESS_TIMEOUT
ARG ARG_SUCCESS_ATTEMPTS
ARG ARG_CURL_RETRY
ARG ARG_CURL_OPTIONS
ARG ARG_CURL_CONNECTION_TIMEOUT
ARG ARG_CURL_RETRY
ARG ARG_CURL_RETRY_DELAY
ARG ARG_CURL_RETRY_MAX_TIME
ENV DOCKER_VERSION 17.09.0-ce
LABEL org.label-schema.schema-version="1.0" \
      org.label-schema.version="$VERSION" \
      org.label-schema.maintainer="https://github.com/capybara1/" \
      org.label-schema.url="https://github.com/capybara1/Docker-Jenkins" \
      org.label-schema.name="jenkins" \
      org.label-schema.license="MIT" \
      org.label-schema.vcs-url="https://github.com/capybara1/Docker-Jenkins" \
      org.label-schema.vcs-ref="$VCS_REF" \
      org.label-schema.build-date="$BUILD_DATE" \
      org.label-schema.dockerfile="/Dockerfile"
COPY plugins.txt /usr/share/jenkins/ref/plugins.txt
RUN set -x; \
    ATTEMPTS="${ARG_ATTEMPTS}" \
    TIMEOUT="${ARG_TIMEOUT}" \
    SUCCESS_TIMEOUT="${ARG_SUCCESS_TIMEOUT}" \
    SUCCESS_ATTEMPTS="${ARG_SUCCESS_ATTEMPTS}" \
    CURL_RETRY="${ARG_CURL_RETRY}" \
    CURL_OPTIONS="${ARG_CURL_OPTIONS}" \
    CURL_CONNECTION_TIMEOUT="${ARG_CURL_CONNECTION_TIMEOUT}" \
    CURL_RETRY="${ARG_CURL_RETRY}" \
    CURL_RETRY_DELAY="${ARG_CURL_RETRY_DELAY}" \
    CURL_RETRY_MAX_TIME="${ARG_CURL_RETRY_MAX_TIME}" \
    /usr/local/bin/install-plugins.sh < /usr/share/jenkins/ref/plugins.txt
USER root
RUN set -x; \
    apk add --no-cache su-exec
RUN set -x; \
    cd /tmp/ \
 && curl -sSL -O https://download.docker.com/linux/static/stable/x86_64/docker-${DOCKER_VERSION}.tgz \
 && tar zxf docker-${DOCKER_VERSION}.tgz \
 && mkdir -p /usr/local/bin/ \
 && mv $(find -name 'docker' -type f) /usr/local/bin/ \
 && chmod +x /usr/local/bin/docker \
 && rm -rf /tmp/*
COPY docker-entrypoint.sh /
ENTRYPOINT ["/docker-entrypoint.sh"]
