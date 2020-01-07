FROM alpine:latest
MAINTAINER sabrsorensen@gmail.com

ARG BUILD_DATE
ARG VCS_REF

LABEL org.label-schema.vcs-ref=$VCS_REF \
      org.label-schema.vcs-url="https://github.com/sabrsorensen/alpine-mono.git" \
      org.label-schema.build-date=$BUILD_DATE

# add the edge testing repo and install mono, curl for healthchecks, and shadow for user/group management.
RUN echo http://dl-4.alpinelinux.org/alpine/edge/testing >> /etc/apk/repositories && \
    apk -U upgrade --no-cache && \
    apk -U add --no-cache \
    ca-certificates \
    curl \
    mono \
    shadow \
    tzdata && \
    cert-sync /etc/ssl/certs/ca-certificates.crt

# install s6-overlay for process management
ADD https://github.com/just-containers/s6-overlay/releases/download/v1.22.1.0/s6-overlay-amd64.tar.gz /tmp/
RUN tar xzf /tmp/s6-overlay-amd64.tar.gz -C /
ENTRYPOINT ["/init"]

# cleanup apk cache
RUN rm -rf /root/.cache /tmp/*
