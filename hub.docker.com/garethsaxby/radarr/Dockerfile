FROM alpine:3.9.3

ENV RADARR_VERSION=0.2.0.1344

RUN apk add --no-cache dumb-init && \
    apk add --no-cache mono --repository http://dl-cdn.alpinelinux.org/alpine/edge/testing && \
    apk add --no-cache --virtual=.build-dependencies ca-certificates && \
    cert-sync /etc/ssl/certs/ca-certificates.crt && \
    apk del .build-dependencies

RUN wget https://github.com/Radarr/Radarr/releases/download/v${RADARR_VERSION}/Radarr.develop.${RADARR_VERSION}.linux.tar.gz \
  -O /tmp/Radarr.develop.${RADARR_VERSION}.linux.tar.gz && \
  cd /tmp && \
  tar xf /tmp/Radarr.develop.${RADARR_VERSION}.linux.tar.gz && \
  mv /tmp/Radarr /opt/radarr && \
  rm -fv /tmp/Radarr.develop.${RADARR_VERSION}.linux.tar.gz

EXPOSE 7878
VOLUME [ "/data" ]

ENTRYPOINT [ "/usr/bin/dumb-init" ]
CMD ["/usr/bin/mono", "/opt/radarr/Radarr.exe", "/nobrowser", "/data=/data"]