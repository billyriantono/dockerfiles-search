FROM alpine as alpine
RUN \
  apk update && \
  apk add --no-cache bash curl git && \
  rm -rf /var/cache/apk/* && \
  mkdir -p /root/.docker && \
  mkdir -p /busybox-integration && \
  mkdir -p /busybox-integration/bin && \
  mkdir -p /busybox-integration/lib && \
  ln -s /alpine/bin/busybox /busybox-integration/bin/ && \
  ln -s /alpine/bin/sh /busybox-integration/bin/ && \
  ln -s /alpine/bin/bash /busybox-integration/bin/ && \
  ln -s /alpine/lib/ld-musl-x86_64.so.1 /busybox-integration/lib/
  
FROM gcr.io/kaniko-project/executor

COPY --from=alpine /busybox-integration/bin /bin
COPY --from=alpine /busybox-integration/lib /lib
COPY --from=alpine / /alpine

# VOLUME /alpine

ENV HOME /root
ENV USER /root
ENV LD_LIBRARY_PATH /alpine/lib:/alpine/usr/lib
ENV PATH /kaniko:/alpine/usr/bin:/alpine/usr/sbin:/alpine/usr/local/bin:/alpine/usr/local/sbin:/alpine/bin:/alpine/sbin
ENV SSL_CERT_DIR=/kaniko/ssl/certs
ENV CURL_CA_BUNDLE=/alpine/etc/ssl/certs/ca-certificates.crt
ENV DOCKER_CONFIG /alpine/root/.docker/
